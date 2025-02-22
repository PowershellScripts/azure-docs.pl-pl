---
title: Rozwiązywanie typowych błędów w Azure Cosmos DB interfejs API Cassandra
description: W tym dokumencie omówiono sposoby rozwiązywania typowych problemów występujących w Azure Cosmos DB interfejs API Cassandra
author: TheovanKraay
ms.service: cosmos-db
ms.subservice: cosmosdb-mongo
ms.topic: troubleshooting
ms.date: 12/01/2020
ms.author: thvankra
ms.openlocfilehash: c969e4fac3ae30088cfe47a7b0edff22c578cb8b
ms.sourcegitcommit: 7e97ae405c1c6c8ac63850e1b88cf9c9c82372da
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/29/2020
ms.locfileid: "97802375"
---
# <a name="troubleshoot-common-issues-in-azure-cosmos-db-cassandra-api"></a>Rozwiązywanie typowych problemów z Azure Cosmos DB interfejs API Cassandra
[!INCLUDE[appliesto-cassandra-api](includes/appliesto-cassandra-api.md)]

Interfejs API Cassandra w Azure Cosmos DB to warstwa zgodności, która zapewnia [obsługę protokołu przewodowego](cassandra-support.md) dla popularnej bazy danych Apache Cassandra typu open source i jest obsługiwane przez [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction). Jako w pełni zarządzana usługa w chmurze, Azure Cosmos DB zapewnia [gwarancje dotyczące dostępności, przepływności i spójności](https://azure.microsoft.com/support/legal/sla/cosmos-db/v1_3/) interfejs API Cassandra. Te gwarancje nie są możliwe w starszych implementacjach platformy Apache Cassandra. Interfejs API Cassandra ułatwia również wykonywanie operacji na platformie o zerowej konserwacji i stosowanie poprawek bez przestojów. W związku z tym wiele operacji zaplecza jest różna od platformy Apache Cassandra, dlatego zalecamy określone ustawienia i podejścia, aby uniknąć typowych błędów. 

W tym artykule opisano typowe błędy i rozwiązania dla aplikacji korzystających z Azure Cosmos DB interfejs API Cassandra.

## <a name="common-errors-and-solutions"></a>Typowe błędy i rozwiązania

| Błąd               |  Opis             | Rozwiązanie  |
|---------------------|--------------------------|-----------|
| Załadowaneexception (Java) | Całkowita liczba zużytych jednostek żądania jest większa niż jednostka żądania obsługiwana w obszarze kluczy lub tabeli. Żądania są ograniczone. | Rozważ przeskalowanie przepływności przypisanej do przestrzeni kluczy lub tabeli z Azure Portal (zobacz [tutaj](manage-scale-cassandra.md) , aby skalować operacje w interfejs API Cassandra), lub Zaimplementuj zasady ponawiania. W przypadku języka Java Zobacz przykłady ponownych prób dla sterownika [v3. x](https://github.com/Azure-Samples/azure-cosmos-cassandra-java-retry-sample) i [v4. x](https://github.com/Azure-Samples/azure-cosmos-cassandra-java-retry-sample-v4). Zobacz również [rozszerzenia usługi Azure Cosmos Cassandra dla języka Java](https://github.com/Azure/azure-cosmos-cassandra-extensions) |
| Załadowaneexception (Java) nawet z wystarczającą przepływność | System wydaje się ograniczać żądania, mimo że jest wystarczająca przepływność dla woluminu żądania i/lub zużytego kosztu jednostki żądania  | Interfejs API Cassandra implementuje budżet przepływności systemu dla operacji na poziomie schematu (CREATE TABLE, ALTER TABLE, DROP TABLE). Ten budżet powinien być wystarczający dla operacji schematu w systemie produkcyjnym. Jeśli jednak masz dużą liczbę operacji na poziomie schematu, możliwe jest przekroczenie tego limitu. Ponieważ ten budżet nie jest kontrolowany przez użytkownika, należy rozważyć zmniejszenie liczby uruchamianych operacji schematu. Jeśli wykonanie tej akcji nie rozwiąże problemu lub nie jest to możliwe w obciążeniu, [Utwórz żądanie pomocy technicznej platformy Azure](../azure-portal/supportability/how-to-create-azure-support-request.md).|
| ClosedConnectionException (Java) | Po upływie czasu bezczynności po pomyślnym nawiązaniu połączenia aplikacja nie może nawiązać połączenia| Ten błąd może być spowodowany limitem czasu bezczynności LoadBalancers platformy Azure, który wynosi 4 minuty. Ustaw ustawienie utrzymywanie aktywności w sterowniku (zobacz poniżej) i zwiększ ustawienia utrzymywania aktywności w systemie operacyjnym lub [Dostosuj limit czasu bezczynności w Azure Load Balancer](../load-balancer/load-balancer-tcp-idle-timeout.md?tabs=tcp-reset-idle-portal). |
| Inne sporadyczne błędy łączności (Java) | Nieoczekiwanie wystąpiło lub upłynął limit czasu połączenia | Sterowniki Apache Cassandra dla języka Java zapewniają dwie natywne zasady ponownego połączenia: `ExponentialReconnectionPolicy` i `ConstantReconnectionPolicy` . Wartość domyślna to `ExponentialReconnectionPolicy`. Jednakże w przypadku Azure Cosmos DB interfejs API Cassandra zalecamy `ConstantReconnectionPolicy` opóźnienie wynoszące 2 sekundy. Zobacz [dokumentację sterowników](https://docs.datastax.com/en/developer/java-driver/4.9/manual/core/reconnection/)  dla sterownika Java v4. x i [tutaj](https://docs.datastax.com/en/developer/java-driver/3.7/manual/reconnection/) , aby poznać wskazówki dotyczące języka Java 3. x (Zobacz również przykłady poniżej).|

Jeśli błąd nie jest wymieniony powyżej i wystąpił błąd podczas wykonywania [obsługiwanej operacji w interfejs API Cassandra, w](cassandra-support.md)której wystąpił błąd *podczas korzystania z natywnego elementu Apache Cassandra*, [Utwórz żądanie pomocy technicznej platformy Azure](../azure-portal/supportability/how-to-create-azure-support-request.md)

## <a name="configuring-reconnectionpolicy-for-java-driver"></a>Konfigurowanie ReconnectionPolicy dla sterownika Java

### <a name="version-3x"></a>Wersja 3. x

W przypadku wersji 3. x sterownika Java Skonfiguruj zasady ponownego połączenia podczas tworzenia obiektu klastra:

```java
import com.datastax.driver.core.policies.ConstantReconnectionPolicy;

Cluster.builder()
  .withReconnectionPolicy(new ConstantReconnectionPolicy(2000))
  .build();
```

### <a name="version-4x"></a>4. x

W przypadku wersji 4. x sterownika Java Skonfiguruj zasady ponownego połączenia, zastępując ustawienia w `reference.conf` pliku:

```xml
datastax-java-driver {
  advanced {
    reconnection-policy{
      # The driver provides two implementations out of the box: ExponentialReconnectionPolicy and
      # ConstantReconnectionPolicy. We recommend ConstantReconnectionPolicy for Cassandra API, with 
      # base-delay of 2 seconds.
      class = ConstantReconnectionPolicy
      base-delay = 2 second
    }
}
```

## <a name="enable-keep-alive-for-java-driver"></a>Włącz funkcję Keep-Alive dla sterownika Java

### <a name="version-3x"></a>Wersja 3. x

W przypadku wersji 3. x sterownika Java ustaw wartość Keep-Alive podczas tworzenia obiektu klastra i upewnij się, [że w systemie operacyjnym włączona jest funkcja](https://knowledgebase.progress.com/articles/Article/configure-OS-TCP-KEEPALIVE-000080089)Keep-Alive:

```java
import java.net.SocketOptions;
    
SocketOptions options = new SocketOptions();
options.setKeepAlive(true);
cluster = Cluster.builder().addContactPoints(contactPoints).withPort(port)
  .withCredentials(cassandraUsername, cassandraPassword)
  .withSocketOptions(options)
  .build();
```

### <a name="version-4x"></a>4. x

W przypadku wersji 4. x sterownika Java ustaw wartość Keep-Alive, zastępując ustawienia w `reference.conf` i upewnij się, że [w systemie operacyjnym włączona jest funkcja](https://knowledgebase.progress.com/articles/Article/configure-OS-TCP-KEEPALIVE-000080089)Keep-Alive:

```xml
datastax-java-driver {
  advanced {
    socket{
      keep-alive = true
    }
}
```

## <a name="next-steps"></a>Następne kroki

- Poznaj [obsługiwane funkcje](cassandra-support.md) w Azure Cosmos DB interfejs API Cassandra.
- Dowiedz się, jak [przeprowadzić migrację z macierzystego Cassandra Apache do Azure Cosmos DB interfejs API Cassandra](cassandra-migrate-cosmos-db-databricks.md)


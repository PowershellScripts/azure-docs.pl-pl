---
title: Pobierz punkty końcowe dla rejestracji aplikacji usługi Azure AD
titleSuffix: Microsoft identity platform
description: Jak znaleźć punkty końcowe uwierzytelniania dla aplikacji niestandardowej, którą tworzysz lub rejestrujesz w usłudze Azure AD.
services: active-directory
author: rwike77
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.custom: aaddev
ms.workload: identity
ms.topic: conceptual
ms.date: 05/07/2020
ms.author: ryanwi
ROBOTS: NOINDEX
ms.openlocfilehash: 3afaf654228511a357461a9e762be0b04acc65c6
ms.sourcegitcommit: 2488894b8ece49d493399d2ed7c98d29b53a5599
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/11/2021
ms.locfileid: "98064168"
---
# <a name="how-to-discover-endpoints"></a>Jak odnajdywać punkty końcowe

Punkty końcowe uwierzytelniania dla aplikacji można znaleźć w [Azure Portal](https://portal.azure.com).

1. Zaloguj się do <a href="https://portal.azure.com/" target="_blank">Azure Portal <span class="docon docon-navigate-external x-hidden-focus"></span> </a>.
1. Wybierz pozycję **Azure Active Directory**.
1. W obszarze **Zarządzaj** wybierz pozycję **rejestracje aplikacji**, a następnie wybierz pozycję **punkty końcowe** w górnym menu.

    Zostanie wyświetlona strona **punkty końcowe** przedstawiające punkty końcowe uwierzytelniania dla dzierżawy.
    
    Użyj punktu końcowego, który jest zgodny z protokołem uwierzytelniania używanym w połączeniu z **identyfikatorem aplikacji (klienta)** , aby wystawić żądanie uwierzytelniania specyficzne dla aplikacji.

**Chmury narodowe** (na przykład Azure AD Chiny, Niemcy i Administracja USA) mają własny portal rejestracji aplikacji i punkty końcowe uwierzytelniania usługi Azure AD. Więcej informacji znajduje się w temacie [Omówienie chmur krajowych](authentication-national-cloud.md).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat punktów końcowych w różnych środowiskach platformy Azure, zobacz [Omówienie chmur krajowych](authentication-national-cloud.md).

---
title: Istruzioni online
permalink: index.html
layout: home
ms.openlocfilehash: 8cc220d44fe56f19385b25675c29e391b610db8e
ms.sourcegitcommit: d2d374fffa4fcbf92b9c4bdc9c9ecc470152e033
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/16/2021
ms.locfileid: "132626087"
---
## <a name="content-directory"></a>Directory contenuto

In basso sono elencati i collegamenti ipertestuali a tutti i lab.

## <a name="labs"></a>Lab

{% assign labs = site.pages | where_exp: "page", "page.url contains '/Instructions/Labs'" %}
| Modulo | Lab |
| --- | --- |
{% for activity in labs  %}{% if activity.lab.az204Module %}}| {{ activity.lab.az204Module }} | [{{ activity.lab.az204Title }}]({{ site.github.url }}{{ activity.url }}) |
{% endif %}{% endfor %}

## <a name="demos"></a>Demo

{% assign demos = site.pages | where_exp:"page", "page.url contains '/Instructions/Demos'" %}
| Modulo | Demo |
| --- | --- | 
{% for activity in demos  %}| {{ activity.demo.az204Module }} | [{{ activity.demo.az204Title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}

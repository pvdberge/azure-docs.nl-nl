---
title: Naslag informatie over Azure Service Bus SQLFilter | Microsoft Docs
description: Dit artikel bevat informatie over SQLFilter-grammatica. Een SqlFilter ondersteunt een subset van de SQL-92-standaard.
ms.topic: article
ms.date: 06/23/2020
ms.openlocfilehash: 8412dea583ae119b30976e53d4751411b45339a4
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85341592"
---
# <a name="sqlfilter-syntax"></a>SQLFilter-syntaxis

Een *SqlFilter* -object is een instantie van de [klasse SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)en vertegenwoordigt een op SQL-taal gebaseerde filter expressie die wordt geëvalueerd op basis van een [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). Een SqlFilter ondersteunt een subset van de SQL-92-standaard.  
  
 In dit onderwerp vindt u meer informatie over SqlFilter-grammatica.  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a>Argumenten  
  
-   `<scope>`is een optionele teken reeks die het bereik van de aangeeft `<property_name>` . Geldige waarden zijn `sys` of `user` . De `sys` waarde geeft de systeem Scope aan waar de `<property_name>` naam van een open bare eigenschap van de [klasse BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)is. `user`Hiermee wordt het gebruikers bereik aangegeven waarbij `<property_name>` een sleutel van de [BrokeredMessage-klassen](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) woordenlijst is. `user`Scope is het standaard bereik als `<scope>` niet is opgegeven.  
  
## <a name="remarks"></a>Opmerkingen

Er is een fout opgetreden bij een poging toegang te krijgen tot een niet-bestaande systeem eigenschap. een poging om toegang te krijgen tot een niet-bestaande gebruikers eigenschap is geen fout. In plaats daarvan wordt een niet-bestaande gebruikers eigenschap intern geëvalueerd als een onbekende waarde. Een onbekende waarde wordt speciaal behandeld tijdens de evaluatie van de operator.  
  
## <a name="property_name"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Argumenten  

 `<regular_identifier>`is een teken reeks die wordt vertegenwoordigd door de volgende reguliere expressie:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
Deze grammatica betekent dat een wille keurige teken reeks begint met een letter en wordt gevolgd door een of meer onderstrepings tekens/letter/cijfer.  
  
`[:IsLetter:]`betekent elk Unicode-teken dat is gecategoriseerd als Unicode-letter. `System.Char.IsLetter(c)`retourneert `true` `c` een Unicode-letter.  
  
`[:IsDigit:]`betekent elk Unicode-teken dat is gecategoriseerd als een decimaal cijfer. `System.Char.IsDigit(c)`retourneert `true` of `c` een Unicode-cijfer is.  
  
Een `<regular_identifier>` kan geen gereserveerd tref woord zijn.  
  
`<delimited_identifier>`is een teken reeks die wordt Inge sloten met vier Kante haken links/rechts ([]). Een rechter rechte haak wordt weer gegeven als twee rechter rechte haken. Hier volgen enkele voor beelden van `<delimited_identifier>` :  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>`is een teken reeks die tussen dubbele aanhalings tekens is geplaatst. Een dubbel aanhalings teken in id wordt weer gegeven als twee dubbele aanhalings tekens. Het is niet raadzaam om id's van aanhalings tekens te gebruiken omdat deze eenvoudig kunnen worden verward met een teken reeks constante. Gebruik, indien mogelijk, een gescheiden id. Hier volgt een voor beeld van `<quoted_identifier>` :  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>pattern  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Opmerkingen
  
`<pattern>`moet een expressie zijn die als een teken reeks wordt geëvalueerd. Deze wordt gebruikt als een patroon voor de LIKE-operator.      De naam kan de volgende joker tekens bevatten:  
  
-   `%`: Een wille keurige teken reeks van nul of meer tekens.  
  
-   `_`: Eén wille keurig teken.  
  
## <a name="escape_char"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Opmerkingen  

`<escape_char>`moet een expressie zijn die als een teken reeks met een lengte van 1 wordt geëvalueerd. Deze wordt gebruikt als escape-teken voor de operator LIKE.  
  
 Bijvoorbeeld, `property LIKE 'ABC\%' ESCAPE '\'` komt overeen met `ABC%` een teken reeks die begint met `ABC` .  
  
## <a name="constant"></a>bedrag  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Argumenten  
  
-   `<integer_constant>`is een teken reeks die niet tussen aanhalings tekens staat en geen decimale punten bevat. De waarden worden intern opgeslagen `System.Int64` en volgen hetzelfde bereik.  
  
     Dit zijn voor beelden van lange constanten:  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>`is een teken reeks die niet tussen aanhalings tekens staat en een decimaal teken bevat. De waarden worden intern opgeslagen `System.Double` en volgen hetzelfde bereik/dezelfde precisie.  
  
     In een toekomstige versie kan dit nummer worden opgeslagen in een ander gegevens type ter ondersteuning van nauw keurige semantiek, dus moet u niet vertrouwen op het feit dat het onderliggende gegevens type `System.Double` voor is `<decimal_constant>` .  
  
     Hier volgen enkele voor beelden van decimale constanten:  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>`is een getal dat is geschreven in een weten schappelijke notatie. De waarden worden intern opgeslagen `System.Double` en volgen hetzelfde bereik/dezelfde precisie. Hier volgen enkele voor beelden van constanten met een benaderende waarde:  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="boolean_constant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Opmerkingen  

Booleaanse constanten worden vertegenwoordigd door de tref woorden **True** of **False**. De waarden worden opgeslagen als `System.Boolean` .  
  
## <a name="string_constant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Opmerkingen  

Teken reeks constanten worden tussen enkele aanhalings tekens geplaatst en bevatten geldige Unicode-tekens. Een enkel aanhalings teken in een teken reeks constante wordt weer gegeven als twee enkele aanhalings tekens.  
  
## <a name="function"></a>-functie  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Opmerkingen
  
De `newid()` functie retourneert een **System. GUID** die is gegenereerd door de- `System.Guid.NewGuid()` methode.  
  
De `property(name)` functie retourneert de waarde van de eigenschap waarnaar wordt verwezen door `name` . De `name` waarde kan een geldige expressie zijn die een teken reeks waarde retourneert.  
  
## <a name="considerations"></a>Overwegingen
  
Houd rekening met de volgende [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) -semantiek:  
  
-   Eigenschaps namen zijn niet hoofdletter gevoelig.  
  
-   Opera tors volgen impliciete semantische conversies van C# als dat mogelijk is.  
  
-   Systeem eigenschappen zijn open bare eigenschappen die worden weer gegeven in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) -instanties.  
  
    Houd rekening met de volgende `IS [NOT] NULL` semantiek:  
  
    -   `property IS NULL`wordt geëvalueerd alsof `true` de eigenschap niet bestaat of de waarde van de eigenschap is `null` .  
  
### <a name="property-evaluation-semantics"></a>Semantische eigenschappen van eigenschaps evaluatie  
  
- Een poging om een niet-bestaande systeem eigenschap te evalueren, genereert een [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) -uitzonde ring.  
  
- Een eigenschap die niet bestaat, wordt intern geëvalueerd als **onbekend**.  
  
  Onbekende evaluatie van reken kundige Opera tors:  
  
- Voor binaire Opera tors geldt dat als de linker-en/of rechter zijde van operands wordt geëvalueerd als **onbekend**, het resultaat **onbekend**is.  
  
- Voor unaire Opera tors geldt dat als een operand als **onbekend**wordt geëvalueerd, het resultaat **onbekend**is.  
  
  Onbekende evaluatie van Opera tors voor binaire vergelijkings operatoren:  
  
- Als de linker-en/of rechter zijde van operands wordt geëvalueerd als **onbekend**, is het resultaat **onbekend**.  
  
  Onbekende evaluatie in `[NOT] LIKE` :  
  
- Als een operand als **onbekend**wordt geëvalueerd, is het resultaat **onbekend**.  
  
  Onbekende evaluatie in `[NOT] IN` :  
  
- Als de linkeroperand wordt geëvalueerd als **onbekend**, is het resultaat **onbekend**.  
  
  Onbekende evaluatie in **en** -operator:  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 Onbekende evaluatie in **of** -operator:  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a>Semantiek van operator binding
  
-   Vergelijkings operatoren zoals,,,, `>` `>=` `<` `<=` `!=` en `=` volgen dezelfde semantiek als de C#-operator die is gebonden aan het type van de aantekening van gegevens typen en impliciete conversies.  
  
-   Reken kundige Opera tors zoals,,, `+` `-` `*` `/` en `%` volgen dezelfde semantiek als de C#-operator die is gebonden aan het gegevens type promoties en impliciete conversies.

## <a name="next-steps"></a>Volgende stappen

- [SQLFilter-klasse (.NET Framework)](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [SQLFilter-klasse (.NET Standard)](/dotnet/api/microsoft.azure.servicebus.sqlfilter)
- [Klasse SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)

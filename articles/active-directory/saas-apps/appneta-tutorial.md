---
title: 'Zelfstudie: Eenmalige aanmelding van Azure Active Directory integreren met AppNeta Performance Monitor | Microsoft Docs'
description: Ontdek hoe u eenmalige aanmelding configureert tussen Azure Active Directory en AppNeta Performance Monitor.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 11/06/2019
ms.author: jeedes
ms.openlocfilehash: 5100974c071d6a63fd2c00e496a5422fef2dffb9
ms.sourcegitcommit: 023d10b4127f50f301995d44f2b4499cbcffb8fc
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88517633"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-appneta-performance-monitor"></a>Zelfstudie: Eenmalige aanmelding van Azure Active Directory integreren met AppNeta Performance Monitor

In deze zelfstudie leert u hoe u AppNeta Performance Monitor kunt integreren met Azure AD (Active Directory). Wanneer u AppNeta Performance Monitor integreert met Azure AD, kunt u het volgende doen:

* In Azure AD beheren wie toegang heeft tot AppNeta Performance Monitor.
* U kunt instellen dat gebruikers automatisch met hun Azure AD-account worden aangemeld bij AppNeta Performance Monitor.
* Uw accounts op een centrale locatie beheren: Azure Portal.

Zie [Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis) voor meer informatie over de integratie van SaaS-apps met Azure AD.

## <a name="prerequisites"></a>Vereisten

U hebt het volgende nodig om aan de slag te gaan:

* Een Azure AD-abonnement Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).
* Een AppNeta-abonnement waarvoor eenmalige aanmelding is ingeschakeld.

## <a name="scenario-description"></a>Scenariobeschrijving

In deze zelfstudie gaat u in een testomgeving eenmalige aanmelding van Azure AD configureren en testen.

* AppNeta Performance Monitor ondersteunt door **SP** geïnitieerde eenmalige aanmelding


* AppNeta Performance Monitor ondersteunt het **Just-In-Time** inrichten van gebruikers

> [!NOTE]
> De id van deze toepassing is een vaste tekenreekswaarde zodat maar één exemplaar in één tenant kan worden geconfigureerd.


## <a name="adding-appneta-performance-monitor-from-the-gallery"></a>AppNeta Performance Monitor toevoegen vanuit de galerie

Als u de integratie van AppNeta Performance Monitor met Azure AD wilt configureren, moet u AppNeta Performance Monitor toevoegen vanuit de galerie aan uw lijst van beheerde SaaS-apps.

1. Meld u bij de [Azure-portal](https://portal.azure.com) aan met een werk- of schoolaccount of een persoonlijk Microsoft-account.
1. Selecteer in het linkernavigatiedeelvenster de service **Azure Active Directory**.
1. Ga naar **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **Nieuwe toepassing** om een nieuwe toepassing toe te voegen.
1. Typ in de sectie **Toevoegen vanuit de galerie** in het zoekvak: **AppNeta Performance Monitor**.
1. Selecteer **AppNeta Performance Monitor** in het resultatenpaneel en voeg de app vervolgens toe. Wacht enkele seconden tot de app is toegevoegd aan de tenant.


## <a name="configure-and-test-azure-ad-single-sign-on-for-appneta-performance-monitor"></a>Eenmalige aanmelding van Azure AD configureren en testen voor AppNeta Performance Monitor

Configureer en test eenmalige aanmelding van Azure AD met AppNeta Performance Monitor met behulp van een testgebruiker met de naam **B.Simon**. Eenmalige aanmelding werkt alleen als u een koppelingsrelatie tot stand brengt tussen een Azure AD-gebruiker en de gerelateerde gebruiker in AppNeta Performance Monitor.

Als u eenmalige aanmelding van Azure AD met AppNeta Performance Monitor wilt configureren en testen, moet u de volgende bouwstenen voltooien:

1. **[Eenmalige aanmelding van Azure AD configureren](#configure-azure-ad-sso)** : zodat uw gebruikers deze functie kunnen gebruiken.
    1. **[Een Azure AD-testgebruiker maken](#create-an-azure-ad-test-user)** : om eenmalige aanmelding van Azure AD te testen met B.Simon.
    1. **[De Azure AD-testgebruiker toewijzen](#assign-the-azure-ad-test-user)** zodat B.Simon eenmalige aanmelding van Azure AD kan gebruiken.
1. **[Eenmalige aanmelding met AppNeta Performance Monitor configureren](#configure-appneta-performance-monitor-sso)** : als u de instellingen voor eenmalige aanmelding aan de toepassingszijde wilt configureren.
    1. **[Een testgebruiker voor AppNeta Performance Monitor maken](#create-appneta-performance-monitor-test-user)** : als u een tegenhanger van B.Simon in AppNeta Performance Monitor wilt hebben die is gekoppeld aan de Azure AD-weergave van de gebruiker.
1. **[Eenmalige aanmelding testen](#test-sso)** : om te controleren of de configuratie werkt.

## <a name="configure-azure-ad-sso"></a>Eenmalige aanmelding van Azure AD configureren

Volg deze stappen om eenmalige aanmelding van Azure AD in te schakelen in Azure Portal.

1. Ga in de [Azure-portal](https://portal.azure.com/) op de integratiepagina van de toepassing **AppNeta Performance Monitor** naar de sectie **Beheren**, en selecteer **Eenmalige aanmelding**.
1. Selecteer **SAML** op de pagina **Selecteer een methode voor eenmalige aanmelding**.
1. Op de pagina **Eenmalige aanmelding instellen met SAML** klikt u op het bewerkings-/penpictogram voor **Standaard-SAML-configuratie** om de instellingen te bewerken.

   ![Standaard SAML-configuratie bewerken](common/edit-urls.png)

1. In de sectie **Standaard-SAML-configuratie** voert u de waarden in voor de volgende velden:

    a. In het tekstvak **Aanmeldings-URL** typt u een URL met de volgende notatie: `https://<subdomain>.pm.appneta.com`

    b. Typ een waarde in het vak **Id (Entiteits-id)** : `PingConnect`

    > [!NOTE]
    > De waarde voor de aanmeldings-URL is niet echt. Werk deze waarde bij met de werkelijke aanmeldings-URL. Neem contact op met [het ondersteuningsteam van AppNeta Performance Monitor](mailto:support@appneta.com) om deze waarde op te halen. U kunt ook verwijzen naar het patroon dat wordt weergegeven in de sectie **Standaard SAML-configuratie** in de Azure-portal.

1. In de AppNeta Performance Monitor-toepassing worden de SAML-asserties in een specifieke indeling verwacht. Hiervoor moet u aangepaste kenmerktoewijzingen toevoegen aan de configuratie van uw SAML-tokenkenmerken. In de volgende schermafbeelding wordt de lijst met standaardkenmerken weergegeven.

    ![image](common/edit-attribute.png)

1. Bovendien worden in de AppNeta Performance Monitor-toepassing nog enkele kenmerken verwacht die als SAML-antwoord moeten worden doorgestuurd. Deze worden hieronder weergegeven. Deze kenmerken worden ook vooraf ingevuld, maar u kunt ze herzien volgens uw vereisten.

    | Naam | Bronkenmerk|
    | --------| ----------------|
    | voornaam| user.givenname|
    | achternaam| user.surname|
    | e-mail| user.userprincipalname|
    | naam| user.userprincipalname|
    | groepen  | user.assignedroles |
    | telefoon| user.telephonenumber |
    | titel| user.jobtitle|
    | | |

    > [!NOTE]
    > **groepen** verwijst naar de beveiligingsgroep in Appneta die is toegewezen aan een **rol** in Azure AD. Raadpleeg [dit](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-app-role-management) doc-bestand waarin wordt uitgelegd hoe u aangepaste rollen maakt in Azure AD.

    1. Klik op **Nieuwe claim toevoegen** om het dialoogvenster **Gebruikersclaims beheren** te openen.

    1. In het tekstvak **Naam** typt u de naam van het kenmerk die voor die rij wordt weergegeven.

    1. Laat **Naamruimte** leeg.

    1. Selecteer Bron bij **Kenmerk**.

    1. Typ de kenmerkwaarde voor die rij in de lijst met **bronkenmerken**.

    1. Klik op **OK**.

    1. Klik op **Opslaan**.

1. Ga op de pagina **Eenmalige aanmelding met SAML instellen** in de sectie **SAML-handtekeningcertificaat** naar **XML-bestand met federatieve metagegevens** en selecteer **Downloaden** om het certificaat te downloaden. Sla dit vervolgens op de computer op.

    ![De link om het certificaat te downloaden](common/metadataxml.png)

1. Kopieer in de sectie **AppNeta Performance Monitor instellen** de juiste URL('s) op basis van uw behoeften.

    ![Configuratie-URL's kopiëren](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

In deze sectie gaat u een testgebruiker met de naam B.Simon maken in Azure Portal.

1. Selecteer in het linkerdeelvenster van Azure Portal de optie **Azure Active Directory**, selecteer **Gebruikers** en selecteer vervolgens **Alle gebruikers**.
1. Selecteer **Nieuwe gebruiker** boven aan het scherm.
1. Volg de volgende stappen bij de eigenschappen voor **Gebruiker**:
   1. Voer in het veld **Naam**`B.Simon` in.  
   1. Voer username@companydomain.extension in het veld **Gebruikersnaam** in. Bijvoorbeeld `B.Simon@contoso.com`.
   1. Schakel het selectievakje **Wachtwoord weergeven** in en noteer de waarde die wordt weergegeven in het vak **Wachtwoord**.
   1. Klik op **Create**.

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie stelt u B.Simon in staat gebruik te maken van eenmalige aanmelding van Azure door haar toegang te verlenen tot AppNeta Performance Monitor.

1. Selecteer in Azure Portal de optie **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **AppNeta Performance Monitor** in de lijst toepassingen.
1. Zoek op de overzichtspagina van de app de sectie **Beheren** en selecteer **Gebruikers en groepen**.

   ![De koppeling Gebruikers en groepen](common/users-groups-blade.png)

1. Selecteer **Gebruiker toevoegen** en selecteer vervolgens **Gebruikers en groepen** in het dialoogvenster **Toewijzing toevoegen**.

    ![De koppeling Gebruiker toevoegen](common/add-assign-user.png)

1. Selecteer in het dialoogvenster **Gebruikers en groepen** de optie **B.Simon** in de lijst Gebruikers. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Als u een waarde voor een rol verwacht in de SAML-assertie, moet u in het dialoogvenster **Rol selecteren** de juiste rol voor de gebruiker in de lijst selecteren. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Klik in het dialoogvenster **Toewijzing toevoegen** op de knop **Toewijzen**.

## <a name="configure-appneta-performance-monitor-sso"></a>Eenmalige aanmelding met AppNeta Performance Monitor configureren

Als u eenmalige aanmelding aan de zijde van **AppNeta Performance Monitor** wilt configureren, moet u de gedownloade **XML met federatieve metagegevens** en de correcte uit de Microsoft Azure-portal gekopieerde URL's verzenden naar het [AppNeta Performance Monitor-ondersteuningsteam](mailto:support@appneta.com). Het team stelt de instellingen zo in dat de verbinding tussen SAML en eenmalige aanmelding aan beide zijden goed is ingesteld.

### <a name="create-appneta-performance-monitor-test-user"></a>Testgebruiker voor AppNeta Performance Monitor maken

In dit gedeelte wordt een gebruiker met de naam Britta Simon gemaakt in AppNeta Performance Monitor. AppNeta Performance Monitor ondersteunt Just-In-Time-inrichting van gebruikers. Deze functie is standaard ingeschakeld. Er is geen actie-item voor u in deze sectie. Als er nog geen gebruiker in AppNeta Performance Monitor bestaat, wordt er een nieuwe gemaakt na verificatie.

> [!Note]
> Als u handmatig een gebruiker moet maken, neemt u contact op met het [ondersteuningsteam van AppNeta Performance Monitor](mailto:support@appneta.com).

## <a name="test-sso"></a>Eenmalige aanmelding testen 

In deze sectie gaat u uw configuratie van Azure AD-eenmalige aanmelding testen via het toegangsvenster.

Wanneer u in het toegangsvenster op de tegel AppNeta Performance Monitor klikt, wordt u automatisch aangemeld bij het exemplaar van AppNeta Performance Monitor waarvoor u eenmalige aanmelding hebt ingesteld. Zie [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) (Inleiding tot het toegangsvenster) voor meer informatie over het toegangsvenster.

## <a name="additional-resources"></a>Aanvullende bronnen

- [ List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) (Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory)

- [What is application access and single sign-on with Azure Active Directory? ](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis) (Wat is toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?)

- [Wat is voorwaardelijke toegang in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [AppNeta Performance Monitor uitproberen met Azure AD](https://aad.portal.azure.com/)


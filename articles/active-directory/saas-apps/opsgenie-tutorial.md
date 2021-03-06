---
title: 'Zelfstudie: Zelfstudie: Azure Active Directory-integratie met OpsGenie | Microsoft Docs'
description: Leer hoe u eenmalige aanmelding tussen Azure Active Directory en OpsGenie configureert.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/19/2020
ms.author: jeedes
ms.openlocfilehash: 0ebcb746e10ae910c695e52fb053fc5d0b316e70
ms.sourcegitcommit: 023d10b4127f50f301995d44f2b4499cbcffb8fc
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88543904"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-opsgenie"></a>Zelfstudie: Integratie van eenmalige aanmelding van Azure Active Directory met OpsGenie

In deze zelfstudie leert u hoe u OpsGenie integreert met Azure AD (Azure Active Directory). Wanneer u OpsGenie integreert met Azure AD, kunt u het volgende doen:

* In Azure AD beheren wie er toegang heeft tot OpsGenie.
* Ervoor zorgen dat uw gebruikers automatisch met hun Azure AD-account worden aangemeld bij OpsGenie.
* Uw accounts op een centrale locatie beheren: Azure Portal.

Zie [Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on) voor meer informatie over de integratie van SaaS-apps met Azure AD.

## <a name="prerequisites"></a>Vereisten

U hebt het volgende nodig om aan de slag te gaan:

* Een Azure AD-abonnement Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).
* Een abonnement waarvoor eenmalige aanmelding bij OpsGenie is ingeschakeld.

## <a name="scenario-description"></a>Scenariobeschrijving

In deze zelfstudie gaat u in een testomgeving eenmalige aanmelding van Azure AD configureren en testen.

* OpsGenie ondersteunt door **IDP** geïnitieerde eenmalige aanmelding
* Zodra u OpsGenie hebt geconfigureerd, kunt u sessiebeheer afdwingen, waardoor exfiltratie en infiltratie van gevoelige gegevens van uw organisatie in realtime worden beschermd. Sessiebeheer is een uitbreiding van voorwaardelijke toegang. [Meer informatie over het afdwingen van sessiebeheer met Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/proxy-deployment-any-app).

## <a name="adding-opsgenie-from-the-gallery"></a>OpsGenie toevoegen vanuit de galerie

Voor het configureren van de integratie van OpsGenie met Microsoft Azure Active Directory moet u OpsGenie vanuit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

1. Meld u bij de [Azure-portal](https://portal.azure.com) aan met een werk- of schoolaccount of een persoonlijk Microsoft-account.
1. Selecteer in het linkernavigatiedeelvenster de service **Azure Active Directory**.
1. Ga naar **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **Nieuwe toepassing** om een nieuwe toepassing toe te voegen.
1. Typ in de sectie **Toevoegen vanuit de galerie** **OpsGenie** in het zoekvak.
1. Selecteer **OpsGenie** in de resultaten en voeg vervolgens de app toe. Wacht enkele seconden tot de app is toegevoegd aan de tenant.

## <a name="configure-and-test-azure-ad-single-sign-on-for-opsgenie"></a>Eenmalige aanmelding van Azure AD configureren en testen voor OpsGenie

Configureer en test eenmalige aanmelding van Azure AD met OpsGenie met behulp van een testgebruiker met de naam **B.Simon**. Eenmalige aanmelding werkt alleen als u een koppelingsrelatie tot stand brengt tussen een Azure AD-gebruiker en de bijbehorende gebruiker in OpsGenie.

Voltooi de volgende stappen om eenmalige aanmelding van Azure AD met OpsGenie te configureren en te testen:

1. **[Eenmalige aanmelding van Azure AD configureren](#configure-azure-ad-sso)** : zodat uw gebruikers deze functie kunnen gebruiken.
    * **[Een Azure AD-testgebruiker maken](#create-an-azure-ad-test-user)** : om eenmalige aanmelding van Azure AD te testen met B.Simon.
    * **[De Azure AD-testgebruiker toewijzen](#assign-the-azure-ad-test-user)** zodat B.Simon eenmalige aanmelding van Azure AD kan gebruiken.
1. **[Eenmalige aanmelding bij OpsGenie configureren](#configure-opsgenie-sso)** : als u de instellingen voor eenmalige aanmelding aan de toepassingszijde wilt configureren.
    * **[Een OpsGenie-testgebruiker maken](#create-opsgenie-test-user)** : als u een equivalent van B.Simon in OpsGenie wilt hebben dat is gekoppeld aan de Azure AD-weergave van de gebruiker.
1. **[Eenmalige aanmelding testen](#test-sso)** : om te controleren of de configuratie werkt.

## <a name="configure-azure-ad-sso"></a>Eenmalige aanmelding van Azure AD configureren

Volg deze stappen om eenmalige aanmelding van Azure AD in te schakelen in Azure Portal.

1. Zoek in [Azure Portal](https://portal.azure.com/) op de integratiepagina van de toepassing **OpsGenie** de sectie **Beheren** en selecteer **Eenmalige aanmelding**.
1. Selecteer **SAML** op de pagina **Selecteer een methode voor eenmalige aanmelding**.
1. Op de pagina **Eenmalige aanmelding instellen met SAML** klikt u op het bewerkings-/penpictogram voor **Standaard-SAML-configuratie** om de instellingen te bewerken.

   ![Standaard SAML-configuratie bewerken](common/edit-urls.png)

1. In de sectie **Standaard SAML-configuratie** voert u de volgende stappen uit:

    a. In het tekstvak **Id** typt u een URL met het volgende patroon: `https://app.opsginie.com/auth/saml/<UNIQUEID>`

    b. In het tekstvak **Antwoord-URL** typt u een URL met de volgende notatie: `https://app.opsginie.com/auth/saml?id=<UNIQUEID>`

    > [!NOTE]
    > Dit zijn geen echte waarden. Werk deze waarden bij met de werkelijke id en antwoord-URL, zoals later in deze zelfstudie wordt uitgelegd.

5. Op de pagina **Eenmalige aanmelding met SAML instellen** in het gedeelte **SAML-handtekeningcertificaat** klikt u op de kopieerknop om de **URL voor federatieve metagegevens van de app** te kopiëren en slaat u deze op uw computer op.

    ![De link om het certificaat te downloaden](common/copy-metadataurl.png)

1. In de sectie **OpsGenie instellen** kopieert u de juiste URL('s) op basis van uw behoeften.

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

In deze sectie geeft u B.Simon toestemming om eenmalige aanmelding van Azure te gebruiken door toegang te verlenen tot OpsGenie.

1. Selecteer in Azure Portal de optie **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **OpsGenie** in de lijst met toepassingen.
1. Zoek op de overzichtspagina van de app de sectie **Beheren** en selecteer **Gebruikers en groepen**.

   ![De koppeling Gebruikers en groepen](common/users-groups-blade.png)

1. Selecteer **Gebruiker toevoegen** en selecteer vervolgens **Gebruikers en groepen** in het dialoogvenster **Toewijzing toevoegen**.

    ![De koppeling Gebruiker toevoegen](common/add-assign-user.png)

1. Selecteer in het dialoogvenster **Gebruikers en groepen** de optie **B.Simon** in de lijst Gebruikers. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Als u een waarde voor een rol verwacht in de SAML-assertie, moet u in het dialoogvenster **Rol selecteren** de juiste rol voor de gebruiker in de lijst selecteren. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Klik in het dialoogvenster **Toewijzing toevoegen** op de knop **Toewijzen**.

## <a name="configure-opsgenie-sso"></a>Eenmalige aanmelding voor OpsGenie configureren

1. Open een ander browserexemplaar en meld u vervolgens aan bij OpsGenie als beheerder.

2. Klik op **Instellingen**en klik vervolgens op het tabblad **Eenmalige aanmelding** .
   
    ![Eenmalige aanmelding voor OpsGenie](./media/opsgenie-tutorial/tutorial-opsgenie-06.png)

3. Als u eenmalige aanmelding wilt inschakelen, selecteert u **Ingeschakeld**.
   
    ![OpsGenie-instellingen](./media/opsgenie-tutorial/tutorial-opsgenie-07.png) 

4. Klik in de sectie **Provider** op het tabblad **Azure Active Directory**.
   
    ![OpsGenie-instellingen](./media/opsgenie-tutorial/tutorial-opsgenie-08.png) 

5. Voer de volgende stappen uit op de dialoogpagina Azure Active Directory:
   
    ![OpsGenie-instellingen](./media/opsgenie-tutorial/tutorial-opsgenie-09.png)
    
    a. Kopieer de waarde van **App-ID URL** en plak deze in het tekstvak **ID (Entiteits-ID)** in de sectie **Standaard SAML-configuratie** in de Azure-portal.

    a. Kopieer de waarde van de **Antwoord-URL** en plak deze in het tekstvak **Antwoord-URL** in de sectie **Standaard SAML-configuratie** in de Azure-portal.

    a. Plak in het tekstvak **SAML 2.0 Endpoint** de waarde van de **aanmeldings-URL** die u uit de Azure-portal hebt gekopieerd.
    
    b. Plak in het tekstvak **Metagegevens-Url** de waarde van **App-URL voor federatieve metagegevens** die u uit de Azure-portal hebt gekopieerd.
    
    c. Als u eenmalige aanmelding wilt inschakelen, schakelt u de knop **Eenmalige aanmelding inschakelen** in.

    d. Klik op **Instellingen voor eenmalige aanmelding toepassen**.

### <a name="create-opsgenie-test-user"></a>OpsGenie-testgebruiker maken

Het doel van dit gedeelte is het maken van een gebruiker met de naam B.Simon in OpsGenie. 

1. Meld u in een webbrowservenster als beheerder aan bij uw OpsGenie-tenant.

2. Ga naar de Gebruikerslijst door op **Gebruikers** te klikken in het linker deelvenster.
   
    ![OpsGenie-instellingen](./media/opsgenie-tutorial/tutorial-opsgenie-10.png) 

3. Klik op **Add User**.

4. Voer in het dialoogvenster **Add User** de volgende stappen uit:
   
    ![OpsGenie-instellingen](./media/opsgenie-tutorial/tutorial-opsgenie-11.png)
   
    a. Typ in het tekstvak **E-mail** het e-mailadres van B. Simon dat is geregistreerd in Azure Active Directory.
   
    b. Typ **B. Simon** in het tekstvak **Volledige naam**.
   
    c. Klik op **Opslaan**. 

> [!NOTE]
> B. Simon ontvangt een e-mailbericht met instructies voor het instellen van het profiel.

## <a name="test-sso"></a>Eenmalige aanmelding testen 

In deze sectie gaat u uw configuratie van Azure AD-eenmalige aanmelding testen via het toegangsvenster.

Wanneer u op de tegel OpsGenie in het toegangsvenster klikt, wordt u automatisch aangemeld bij het OpsGenie-exemplaar waarvoor u eenmalige aanmelding hebt ingesteld. Zie [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) (Inleiding tot het toegangsvenster) voor meer informatie over het toegangsvenster.

## <a name="additional-resources"></a>Aanvullende bronnen

- [ List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) (Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory)

- [What is application access and single sign-on with Azure Active Directory? ](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on) (Wat is toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?)

- [Wat is voorwaardelijke toegang in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Probeer OpsGenie met Azure AD](https://aad.portal.azure.com/)

- [Wat is sessiebeheer in Microsoft Cloud App Security?](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)
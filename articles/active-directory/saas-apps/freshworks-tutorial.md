---
title: 'Zelfstudie: Integratie van eenmalige aanmelding van Azure Active Directory met Freshworks | Microsoft Docs'
description: Ontdek hoe u eenmalige aanmelding configureert tussen Azure Active Directory en Freshworks.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 10/11/2019
ms.author: jeedes
ms.openlocfilehash: eb59d7ecd6183d144fd275a50f3682a2b961df98
ms.sourcegitcommit: 023d10b4127f50f301995d44f2b4499cbcffb8fc
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88550960"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-freshworks"></a>Zelfstudie: Integratie van eenmalige aanmelding van Azure Active Directory met Freshworks

In deze zelfstudie leert u hoe u Freshworks integreert met Azure Active Directory (Azure AD). Wanneer u Freshworks integreert met Azure AD, kunt u het volgende doen:

* In Azure AD bepalen wie toegang heeft tot Freshworks.
* Ervoor zorgen dat gebruikers zich automatisch met hun Azure AD-account kunnen aanmelden bij Freshworks.
* Uw accounts op een centrale locatie beheren: Azure Portal.

Zie [Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis) voor meer informatie over de integratie van SaaS-apps met Azure AD.

## <a name="prerequisites"></a>Vereisten

U hebt het volgende nodig om aan de slag te gaan:

* Een Azure AD-abonnement Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).
* Een abonnement op Freshworks waarvoor eenmalige aanmelding is ingeschakeld.

> [!NOTE]
> Deze integratie is ook beschikbaar voor gebruik vanuit de Azure AD US Government Cloud-omgeving. U kunt deze toepassing vinden in de toepassingsgalerie van Azure AD US Government Cloud en deze op dezelfde manier configureren als vanuit een openbare cloud.

## <a name="scenario-description"></a>Scenariobeschrijving

In deze zelfstudie gaat u in een testomgeving eenmalige aanmelding van Azure AD configureren en testen.

* Freshworks biedt ondersteuning voor met **SP** geïnitieerde eenmalige aanmelding

## <a name="adding-freshworks-from-the-gallery"></a>Freshworks toevoegen vanuit de galerie

U moet Freshworks uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps om de integratie van Freshworks in Azure AD te configureren.

1. Meld u bij de [Azure-portal](https://portal.azure.com) aan met een werk- of schoolaccount of een persoonlijk Microsoft-account.
1. Selecteer in het linkernavigatiedeelvenster de service **Azure Active Directory**.
1. Ga naar **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **Nieuwe toepassing** om een nieuwe toepassing toe te voegen.
1. Typ in de sectie **Toevoegen uit de galerie** in het zoekvak: **Freshworks**.
1. Selecteer **Freshworks** in het resultatenvenster en voeg de app vervolgens toe. Wacht enkele seconden tot de app is toegevoegd aan de tenant.

## <a name="configure-and-test-azure-ad-single-sign-on-for-freshworks"></a>Eenmalige aanmelding van Azure AD configureren en testen voor Freshworks

Configureer en test eenmalige aanmelding bij Azure AD met Freshworks met behulp van een testgebruiker met de naam **B.Simon**. Eenmalige aanmelding werkt alleen als u een koppelingsrelatie tot stand brengt tussen een Azure AD-gebruiker en de bijbehorende gebruiker in Freshworks.

Voltooi de volgende stappen om eenmalige aanmelding van Azure AD met Freshworks te configureren en te testen:

1. **[Eenmalige aanmelding van Azure AD configureren](#configure-azure-ad-sso)** : zodat uw gebruikers deze functie kunnen gebruiken.
    1. **[Een Azure AD-testgebruiker maken](#create-an-azure-ad-test-user)** : om eenmalige aanmelding van Azure AD te testen met B.Simon.
    1. **[De Azure AD-testgebruiker toewijzen](#assign-the-azure-ad-test-user)** zodat B.Simon eenmalige aanmelding van Azure AD kan gebruiken.
1. **[Eenmalige aanmelding bij Freshworks configureren](#configure-freshworks-sso)** : als u de instellingen voor eenmalige aanmelding aan de toepassingszijde wilt configureren.
    1. **[Een Freshworks-testgebruiker maken](#create-freshworks-test-user)** : als u een equivalent van B.Simon in Freshworks wilt hebben dat is gekoppeld aan de Azure AD-weergave van de gebruiker.
1. **[Eenmalige aanmelding testen](#test-sso)** : om te controleren of de configuratie werkt.

## <a name="configure-azure-ad-sso"></a>Eenmalige aanmelding van Azure AD configureren

Volg deze stappen om eenmalige aanmelding van Azure AD in te schakelen in Azure Portal.

1. Zoek in [Azure Portal](https://portal.azure.com/) op de integratiepagina van de toepassing **Freshworks** de sectie **Beheren** en selecteer **Eenmalige aanmelding**.
1. Selecteer **SAML** op de pagina **Selecteer een methode voor eenmalige aanmelding**.
1. Op de pagina **Eenmalige aanmelding instellen met SAML** klikt u op het bewerkings-/penpictogram voor **Standaard-SAML-configuratie** om de instellingen te bewerken.

   ![Standaard SAML-configuratie bewerken](common/edit-urls.png)

1. In de sectie **Standaard-SAML-configuratie** voert u de waarden in voor de volgende velden:

    a. In het tekstvak **Aanmeldings-URL** typt u een URL met de volgende notatie: `https://<SUBDOMAIN>.freshworks.com/login`

    b. In het tekstvak **Id (Entiteits-id)** typt u een URL met de volgende notatie: `https://<SUBDOMAIN>.freshworks.com/sp/SAML/<MODULE_ID>/metadata`

    > [!NOTE]
    > Dit zijn geen echte waarden. Werk deze waarden bij met de werkelijke aanmeldings-URL en id. Neem contact op met [het klantondersteuningsteam van Freshworks](mailto:support@freshworks.com) om deze waarden op te halen. U kunt ook verwijzen naar het patroon dat wordt weergegeven in de sectie **Standaard SAML-configuratie** in de Azure-portal.

1. Op de pagina **Eenmalige aanmelding met SAML instellen** in de sectie **SAML-handtekeningcertificaat** gaat u naar **Certificaat (Base64)** en selecteert u **Downloaden** om het certificaat te downloaden en op te slaan op uw computer.

    ![De link om het certificaat te downloaden](common/certificatebase64.png)

1. Om de  **Handtekeningopties**  aan te passen aan uw vereisten, klikt u op de knop  **Bewerken**  om het dialoogvenster  **SAML-handtekeningcertificaat**  te openen.

     ![image](common/edit-certificate.png)

     ![Configuratie van Freshworks](./media/freshworks-tutorial/response.png)

    a. Selecteer **SAML-antwoord ondertekenen** voor **Optie voor ondertekening**.

    b. Klik op **Opslaan**.

1. In de sectie **Freshworks instellen** kopieert u de juiste URL('s) op basis van uw vereisten.

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

In deze sectie geeft u B.Simon toestemming om eenmalige aanmelding van Azure te gebruiken door toegang te verlenen tot Freshworks.

1. Selecteer in Azure Portal de optie **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.
1. Selecteer **Freshworks** in de lijst met toepassingen.
1. Zoek op de overzichtspagina van de app de sectie **Beheren** en selecteer **Gebruikers en groepen**.

   ![De koppeling Gebruikers en groepen](common/users-groups-blade.png)

1. Selecteer **Gebruiker toevoegen** en selecteer vervolgens **Gebruikers en groepen** in het dialoogvenster **Toewijzing toevoegen**.

    ![De koppeling Gebruiker toevoegen](common/add-assign-user.png)

1. Selecteer in het dialoogvenster **Gebruikers en groepen** de optie **B.Simon** in de lijst Gebruikers. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Als u een waarde voor een rol verwacht in de SAML-assertie, moet u in het dialoogvenster **Rol selecteren** de juiste rol voor de gebruiker in de lijst selecteren. Klik vervolgens op de knop **Selecteren** onderaan het scherm.
1. Klik in het dialoogvenster **Toewijzing toevoegen** op de knop **Toewijzen**.

## <a name="configure-freshworks-sso"></a>Eenmalige aanmelding van Freshworks configureren

1. Open een nieuw webbrowservenster en meld u als beheerder bij uw bedrijfssite van Freshworks aan en voer de volgende stappen uit:

2. Klik aan de linkerkant van het menu op het  **beveiligingspictogram**  en schakel vervolgens de optie **Eenmalige aanmelding** in en selecteer **Eenmalige aanmelding op basis van SAML** onder **Verificatiemethoden**.

    ![Configuratie van Freshworks](./media/freshworks-tutorial/configure01.png)

3. Voer in het gedeelte **Single sign-on** de volgende stappen uit:

    ![Configuratie van Freshworks](./media/freshworks-tutorial/configure02.png)

    a. Klik op **Copy** om de **Service Provider(SP) Entity ID** voor uw exemplaar te kopiëren en plak deze in het tekstvak **Id (Entiteits-id)** in de sectie **Standaard SAML-configuratie** in de Azure-portal.

    b. Plak in het tekstvak voor de **entiteits-id die door de idP is verstrekt** de waarde van de **Azure AD-id** die u uit Azure Portal hebt gekopieerd.

    c. Plak in het tekstvak voor de **URL voor eenmalige aanmelding op basis van SAML** de waarde van de **aanmeldings-URL** die u uit Azure Portal hebt gekopieerd.

    d. Open het met base64 gecodeerde certificaat in Kladblok, kopieer de inhoud en plak het in het tekstvak **Security certificate**.

    e. Klik op **Opslaan**.

### <a name="create-freshworks-test-user"></a>Freshworks-testgebruiker maken

In dit gedeelte maakt u in Freshworks een gebruiker met de naam B.Simon. Werk samen met het  [klantondersteuningsteam van Freshworks](mailto:support@freshworks.com) om de gebruikers toe te voegen aan het Freshworks-platform. Er moeten gebruikers worden gemaakt en geactiveerd voordat u eenmalige aanmelding kunt gebruiken. 

## <a name="test-sso"></a>Eenmalige aanmelding testen 

In deze sectie gaat u uw configuratie van Azure AD-eenmalige aanmelding testen via het toegangsvenster.

Wanneer u in het toegangsvenster op de tegel Freshworks klikt, wordt u automatisch aangemeld bij de instantie van Freshworks waarvoor u eenmalige aanmelding hebt ingesteld. Zie [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) (Inleiding tot het toegangsvenster) voor meer informatie over het toegangsvenster.

## <a name="additional-resources"></a>Aanvullende bronnen

- [ List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) (Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory)

- [What is application access and single sign-on with Azure Active Directory? ](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis) (Wat is toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?)

- [Wat is voorwaardelijke toegang in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Freshworks gebruiken met Azure AD](https://aad.portal.azure.com/)


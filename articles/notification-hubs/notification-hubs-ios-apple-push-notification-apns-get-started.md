---
title: Notificações por push para aplicativos iOS usando Hubs de Notificação do Azure | Microsoft Docs
description: Neste tutorial, você aprenderá a usar os Hubs de Notificação do Azure para enviar notificações por push a um aplicativo do iOS.
services: notification-hubs
documentationcenter: ios
keywords: notificação por push, notificações por push, notificações por push do ios
author: jwargo
manager: patniko
editor: spelluru
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: tutorial
ms.custom: mvc
ms.date: 01/04/2019
ms.author: jowargo
ms.openlocfilehash: 63fb04e6b31fe4026b93cef09d88601d6182101a
ms.sourcegitcommit: 9b6492fdcac18aa872ed771192a420d1d9551a33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54448302"
---
# <a name="tutorial-push-notifications-to-ios-apps-using-azure-notification-hubs"></a>Tutorial: Enviar notificações por push para aplicativos iOS usando Hubs de Notificação do Microsoft Azure

[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Neste tutorial, você usa os Hubs de Notificação do Azure para enviar notificações por push a um aplicativo do iOS. Você cria um aplicativo do iOS em branco que recebe notificações por push usando o [APNs (Apple Push Notification Service)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).

Neste tutorial, você deve executar as seguintes etapas:

> [!div class="checklist"]
> * Gerar o arquivo de solicitação de assinatura de certificado
> * Solicitar seu aplicativo para notificações por push
> * Criar um perfil de provisionamento para o aplicativo
> * Configurar o hub de notificação para notificações por push do iOS
> * Conectar seu aplicativo do iOS aos hubs de notificação
> * Enviar notificações por push de teste
> * Verifique se seu aplicativo recebe notificações

O código completo deste tutorial pode ser encontrado [no GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Pré-requisitos

* Uma conta ativa do Azure. Se não tiver uma conta, você poderá [criar uma conta gratuita do Azure](https://azure.microsoft.com/free) em apenas alguns minutos.
* [Estrutura de Mensagens do Microsoft Azure]
* Versão mais recente do [Xcode]
* Um dispositivo compatível com o iOS 10 (ou versão posterior)
* [Programa de Desenvolvedores de iOS](https://developer.apple.com/programs/) 
  
 > [!NOTE]
 > Devido aos requisitos de configuração das notificações por push, você deve implantá-las e testá-las em um dispositivo iOS físico (iPhone ou iPad), em vez de usar o Simulador de iOS.
  
A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre os Hubs de Notificação para aplicativos do iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>Configurar o Hub de Notificação para notificações por push do iOS

Nesta seção, você cria um hub de notificação e a configurar a autenticação com APNS usando o certificado push **.p12** que você criou anteriormente. Se você quiser usar um hub de notificação já criado, ignore a etapa 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

### <a name="configure-your-notification-hub-with-apns-information"></a>Configure seu hub de notificações com as informações de APNS

1. Em **Serviços de Notificação**, selecione **Apple (APNS)**.
2. Selecione **Certificado**.
3. Selecione o **ícone arquivo**.
4. Selecione o arquivo **. p12** que você exportou anteriormente.
5. Especifique a **senha** correta.
6. Selecione o modo **Sandbox**. Use a **Produção** apenas se quiser enviar notificações por push aos usuários que adquiriram seu aplicativo na loja.

    ![Configurar certificação do APNS no Portal do Azure][7]

Você configurou agora seu hub de notificação para funcionar com o APNS e você tem as cadeias de conexão para registrar seu aplicativo e enviar notificações por push.

## <a name="connect-your-ios-app-to-notification-hubs"></a>Conectar seu aplicativo do iOS aos Hubs de Notificação

1. No Xcode, crie um novo projeto do iOS e selecione o modelo **Aplicativo de Modo de Exibição Único** .

    ![Xcode - aplicativo de modo de exibição único][8]

2. Ao definir as opções para o novo projeto, lembre-se de usar os mesmos **Nome do Produto** e **Identificador Organizacional** que você usou quando configurou o identificador do pacote no Portal do Desenvolvedor da Apple.

    ![Xcode - opções de projeto][11]

3. No Navegador de Projeto, clique no nome do projeto, clique na guia **Geral** e localize **Assinatura**. Verifique se você selecionou a equipe apropriada para sua conta de Desenvolvedor da Apple. O deverá automaticamente efetuar pull do perfil de provisionamento que você criou anteriormente com base em seu identificador de pacote.

    Se você não vir o novo perfil de provisionamento que você criou no Xcode, tente atualizar os perfis da sua identidade de assinatura. Clique em **Xcode** na barra de menus, em **Preferências**, na guia **Conta**, no botão **Exibir Detalhes**, em sua identidade de assinatura e depois clique no botão Atualizar no canto inferior direito.

    ![Xcode - perfil de provisionamento][9]

4. Selecione a guia **recursos** e verifique se você habilitou as notificações por Push

    ![Xcode – funcionalidades de push][12]

5. Baixe a [Estrutura de Mensagens do Microsoft Azure] e descompacte o arquivo. No Xcode, clique com o botão direito do mouse no projeto e clique na opção **Adicionar Arquivos a** para adicionar a pasta **WindowsAzureMessaging.framework** ao seu projeto do Xcode. Selecione **Opções** e verifique se a opção **Copiar itens se necessário** está selecionada e, em seguida, clique em **Adicionar**.

    ![Descompactar o SDK do Azure][10]

6. Adicione ao projeto um novo arquivo de cabeçalho chamado `HubInfo.h`. Esse arquivo conterá as constantes para o hub de notificação. Adicione as seguintes definições e substitua os espaços reservados da cadeia de caracteres literal pelo *nome do hub* e a *DefaultListenSharedAccessSignature* que você anotou anteriormente.

    ```objc
    #ifndef HubInfo_h
    #define HubInfo_h

        #define HUBNAME @"<Enter the name of your hub>"
        #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"

    #endif /* HubInfo_h */
    ```

7. Abra o arquivo `AppDelegate.h` e adicione as seguintes diretivas de importação:

    ```objc
    #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
    #import <UserNotifications/UserNotifications.h>
    #import "HubInfo.h"
    ```
8. No arquivo `AppDelegate.m`, adicione o código a seguir ao método `didFinishLaunchingWithOptions` de acordo com sua versão do iOS. Esse código registra seu identificador de dispositivo nas APNs:

    ```objc
    UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
        UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];

    [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
    [[UIApplication sharedApplication] registerForRemoteNotifications];
    ```

9. No mesmo arquivo, adicione os métodos a seguir:

    ```objc
        - (void) application:(UIApplication *) application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
        SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                    notificationHubPath:HUBNAME];

        [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
            else {
                [self MessageBox:@"Registration Status" message:@"Registered"];
            }
        }];
        }

    -(void)MessageBox:(NSString *) title message:(NSString *)messageText
    {
        UIAlertController *alert = [UIAlertController alertControllerWithTitle:title message:messageText preferredStyle:UIAlertControllerStyleAlert];
        UIAlertAction *okAction = [UIAlertAction actionWithTitle:@"OK" style:UIAlertActionStyleDefault handler:nil];
        [alert addAction:okAction];
        [[[[UIApplication sharedApplication] keyWindow] rootViewController] presentViewController:alert animated:YES completion:nil];
    }
    ```

    Esse código conecta-se ao hub de notificação usando as informações de conexão que você especificou em HubInfo.h. Esse código fornece o token do dispositivo ao hub de notificação para que o hub de notificação possa enviar notificações.

10. No mesmo arquivo, adicione o seguinte método para exibir um **UIAlert** caso a notificação seja recebida enquanto o aplicativo estiver ativo:

    ```objc
    - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
        NSLog(@"%@", userInfo);
        [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
    }
    ```

11. Compile e execute o aplicativo no dispositivo para verificar se não há falhas.

## <a name="send-test-push-notifications"></a>Enviar notificações por push de teste

Você pode testar o recebimento de notificações no aplicativo com a opção *Envio de Teste* no [Portal do Azure]. Isso envia uma notificação por push de teste para seu dispositivo.

![Portal do Azure – Envio de Teste][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="verify-that-your-app-receives-push-notifications"></a>Verifique se seu aplicativo recebe notificações por push

Para testar as notificações por push no iOS, você deve implantar o aplicativo em um dispositivo iOS físico. Não é possível enviar notificações por push da Apple com o Simulador do iOS.

1. Execute o aplicativo e verifique se o registro foi bem-sucedido e pressione **OK**.

    ![Teste de registro de notificação por push de aplicativo do iOS][33]

2. Em seguida, você pode enviar uma notificação por push de teste do [Portal do Azure], conforme descrito na seção anterior.

3. A notificação por push é enviada a todos os dispositivos que estão registrados para receber as notificações do Hub de Notificação específico.

    ![Teste de recebimento de notificação por push de aplicativo do iOS][35]

## <a name="next-steps"></a>Próximas etapas

Neste exemplo simples, você enviou notificações por push a todos os seus dispositivos iOS registrados. Para saber como enviar notificações por push para dispositivos iOS específicos, vá para o tutorial a seguir:

> [!div class="nextstepaction"]
>[Notificações por push para especificar dispositivos](notification-hubs-ios-xplat-segmented-apns-push-notification.md)

<!-- Images. -->
[6]: ./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png
[7]: ./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png
[12]: ./media/notification-hubs-ios-get-started/notification-hubs-enable-push.png
[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png
[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png

<!-- URLs. -->
[Estrutura de Mensagens do Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkID=799698&clcid=0x409
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md
[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Portal do Azure]: https://portal.azure.com

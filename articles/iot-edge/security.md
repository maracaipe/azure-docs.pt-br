---
title: Estrutura de segurança - Azure IoT Edge | Microsoft Docs
description: Saiba mais sobre a segurança, autenticação e padrões de autorização que foram usados para desenvolver o Azure IoT Edge e devem ser considerados ao projetar sua solução
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 10/05/2017
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.custom: seodec18
ms.openlocfilehash: b174d7f9b4b8438687512a90dc7a65b5649f758a
ms.sourcegitcommit: a512360b601ce3d6f0e842a146d37890381893fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2019
ms.locfileid: "54229875"
---
# <a name="security-standards-for-azure-iot-edge"></a>Padrões de segurança do Azure IoT Edge

Mover seus dados e análises para a borda inteligente cria cenários de risco para os quais o Azure IoT Edge foi desenvolvido para abordar. Os padrões de segurança do IoT Edge visam fornecer flexibilidade para diferentes cenários de implantação e perfis de risco, ao mesmo tempo em que ainda oferece a mesma proteção que você espera de todos os serviços do Azure. 

O Azure IoT Edge é executado em vários tipos e modelos de hardware, dá suporte a vários sistemas operacionais e se aplica a diversos cenários de implantação. A avaliação do risco de um cenário de implantação depende de muitas considerações, incluindo a propriedade da solução, geografia de implantação, confidencialidade de dados, privacidade, requisitos normativos e vertical do aplicativo. Em vez de oferecer soluções concretas para cenários específicos, o IoT Edge é uma estrutura de segurança extensível baseada em princípios bem embasados desenvolvidos para escala. 
 
Este artigo apresenta uma visão geral da estrutura de segurança do IoT Edge. Para obter mais informações, consulte [Protegendo borda inteligente](https://azure.microsoft.com/blog/securing-the-intelligent-edge/).

## <a name="standards"></a>Padrões

Padrões de promovem a facilidade de investigação e facilidade de implementação, ambas fundamentais para a segurança. Uma solução de segurança deve ser útil para investigação sob avaliação para criar confiança e não deve ser um obstáculo à implantação. O design da estrutura para proteger o Azure IoT Edge é baseado em protocolo de segurança comprovados do setor e testados pelo tempo para familiaridade e reutilização. 

## <a name="authentication"></a>Autenticação

Quando você implanta uma solução de IoT, precisa saber que somente atores, dispositivos e componentes confiáveis têm acesso à sua solução. Esse conhecimento oferece accountability segura de participantes para habilitar a base de admissão.  Azure IoT Edge atinge esse conhecimento por meio da autenticação.  O mecanismo primário de autenticação para a plataforma Azure IoT Edge é a autenticação baseada em certificado.  Esse mecanismo é derivado de um conjunto de padrões que regem a infraestrutura de chave pública (PKiX) pelo Internet Engineering Task Force (IETF).     

Todos os dispositivos, módulos e atores que interajam com o dispositivo Azure IoT Edge, seja fisicamente ou por meio de uma conexão de rede, devem ter identidades de certificado exclusivas. Nem todo cenário ou componente pode se prestar à autenticação baseada em certificado. Nesses cenários, a extensibilidade da estrutura de segurança oferece alternativas seguras. 

## <a name="authorization"></a>Autorização

O princípio de privilégios mínimos diz que os usuários e os componentes de um sistema devem ter acesso somente ao conjunto mínimo de recursos e dados necessários para desempenharem suas funções. Dispositivos, módulos e atores devem obter acesso apenas a recursos e dados no seu escopo de permissão e somente quando permitido em termos de arquitetura. Algumas permissões são configuráveis com privilégios suficientes e outros em termos de arquitetura imposta.  Por exemplo, um módulo pode ser autorizado por meio de configuração com privilégios para iniciar uma conexão ao Hub IoT do Azure. No entanto, não há nenhum motivo para um módulo em um dispositivo Azure IoT Edge acessar o gêmeo de um módulo em outro dispositivo Azure IoT Edge.

Outros esquemas de autorização incluem direitos de assinatura de certificado, RBAC (direitos de controle de acesso baseado em função) e outros esquemas de autorização maduros. 

## <a name="attestation"></a>Atestado

Atestado garante a integridade de bits de software.  É importante para a detecção e prevenção de malware.  A estrutura de segurança do Azure IoT Edge classifica Atestado em três categorias principais:

* Atestado estático
* Atestado do tempo de execução
* Atestado do software

### <a name="static-attestation"></a>Atestado estático

Atestado estático verifica a integridade de todos os aplicativos de software em um dispositivo, incluindo sistema operacional, todos os tempos de execução e informações de configuração no dispositivo de inicialização. Ele é conhecido como a inicialização segura. A estrutura de segurança para dispositivos Azure IoT Edge estende a fabricantes e incorpora funcionalidades de hardware seguras que garantem processos de atestado estático. Esses processos incluem inicialização segura e atualização de firmware segura.  Trabalhar em forte colaboração com fornecedores de silício elimina as camadas de firmware supérfluas, minimizando a superfície de ameaça. 

### <a name="runtime-attestation"></a>Atestado do tempo de execução

Depois que um sistema tiver concluído o processo de inicialização segura e estiver em execução, sistemas bem projetados detectarão tentativas de injetar malware e adotarão as contramedidas adequadas. Ataques de malware podem ser direcionado a portas e interfaces do sistema para acessar o sistema. Ou, se atores mal-intencionados tiverem acesso físico a um dispositivo, eles poderão invadir o próprio dispositivo ou usar ataques de temporização para obter acesso. Esse conteúdo mal-intencionado, que pode estar na forma de malware ou de alterações de configuração não autorizadas, é injetado após o processo de inicialização de modo que o atestado estático não o detecte. As contramedidas oferecidas ou impostas pela ajuda de hardware do dispositivo para repelir essas ameaças.  A estrutura de segurança para o Azure IoT Edge explicitamente chama extensões para combater ameaças em tempo de execução.  

### <a name="software-attestation"></a>Atestado do software

Todos os sistemas íntegros, incluindo sistemas de borda inteligente devem aceitar atualizações e patches.  A segurança é importante para processos de atualização, caso contrário, eles podem ser vetores de ameaças potenciais.  A estrutura de segurança para chamadas de Azure IoT Edge atualizações por meio de medida e pacotes para assegurar a integridade e autenticar a fonte dos pacotes assinados.  Esse padrão se aplica a todos os sistemas operacionais e bits de software de aplicativo. 

## <a name="hardware-root-of-trust"></a>Raiz de hardware de confiança

Para muitos dispositivos de borda inteligente, especialmente dispositivos em locais em que possíveis atores mal-intencionados têm acesso físico ao dispositivo, a segurança de hardware do dispositivo é a última defesa para proteção. Hardware resistente a adulterações é crucial para essas implantações. O Azure IoT Edge incentiva os fornecedores de hardware de silício seguro a oferecerem diferentes tipos de raiz de confiança de hardware para acomodar vários perfis de risco e cenários de implantação. A confiança do hardware pode vir de padrões de protocolo de segurança comuns como DICE (Mecanismo de Composição de Identificador de Dispositivo) do Trusted Computing Group e Trusted Platform Module (ISO/IEC 11889). Tecnologias de enclave seguras, como TrustZones e SGX (extensões de proteção de software), também fornecem confiança de hardware. 

## <a name="certification"></a>Certificação

Para ajudar os clientes a tomar decisões informadas quando adquirir dispositivos de Azure IoT Edge para sua implantação, a estrutura de borda de IoT do Azure inclui os requisitos de certificação.  Base para esses requisitos são certificações pertencentes às declarações de segurança e certificações pertencente a validação da implementação de segurança.  Por exemplo, uma certificação de declaração de segurança informa que o dispositivo IoT Edge usa hardware seguro, conhecido como resistir a ataques de inicialização. Certificação uma validação informa se o hardware seguro foi corretamente implementado para oferecer esse valor no dispositivo.  Para manter o princípio de simplicidade, a estrutura tenta manter a carga de certificação mínima.   

## <a name="extensibility"></a>Extensibilidade

Extensibilidade é cidadão de primeira classe na estrutura de segurança Azure IoT Edge.  Com a tecnologia de IoT orientando tipos diferentes de transformações empresariais, faz sentido que a segurança evolua em paralelo para lidar com cenários emergentes.  A estrutura de segurança do Azure IoT Edge começa com uma base sólida na qual ele cria no extensibilidade em diferentes dimensões a serem incluídas: 

* Serviços de segurança de primeira como o serviço de provisionamento do dispositivo para o Azure Hub IoT.
* Serviços de terceiros, como serviços gerenciados de segurança para verticais do aplicativo diferente (como industrial ou serviços de saúde) ou o foco de tecnologia (como a segurança de monitoramento de malha redes ou serviços de certificação de hardware silicon) por meio de uma rede avançada do parceiros.
* Sistemas herdados para incluir o aperfeiçoamento com estratégias de segurança alternativas, como usando a tecnologia segura diferente de certificados para autenticação e gerenciamento de identidades.
* Proteger o hardware para a adoção de novas tecnologias de hardware seguro e contribuições de parceiro de silício.

No final, o sucesso mais alto na proteção da borda inteligente resultados de colaboração contribuições da comunidade aberta acompanhando o interesse comum na proteção de IoT.  Essas contribuições podem ser na forma de tecnologias seguras ou serviços.  A estrutura de segurança Azure IoT Edge oferece uma base sólida para a segurança é extensível para a cobertura de máximo oferecer o mesmo nível de confiança e integridade na borda inteligente como com a nuvem do Azure.  

## <a name="next-steps"></a>Próximas etapas

.Leia mais sobre como o Azure IoT Edge é [protegendo a borda inteligente](https://azure.microsoft.com/blog/securing-the-intelligent-edge/).

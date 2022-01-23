# LAB 4 - Utilizando a plataforma Oracle DevOps para construir uma aplicação containerizada em OCI
**Objetivo deste Lab:**

Nesta etapa construirá uma esteira de desenvolvimento capaz de entregar uma aplicação containerizada, de forma automatizada, a um cluster Kubernetes!

**Você aprenderá todo o passo-a-passo dessa implementação:**
 - [Pre Reqs: Executar terraform de preparação de ambiente, e coletar informações relevantes ao processo](#PreReqs)
 - [Passo 1: Clonar o repositório e movimentar conteúdo para repositório do projeto DevOps](#Passo1)
 - [Passo 2: Criar e configurar processo de construção (CI)](#Passo2)
 - [Passo 3: Criar e configurar entrega de artefatos (CI)](#Passo3)
 - [Passo 4: Criar e configurar entrega de aplicação a cluster kubernetes (CD)](#Passo4)
 - [Passo 5: Configurar gatilho do fluxo e conectar pipelines de CI/CD](#Passo5)
 - [Passo 6: Execução e testes](#Passo6)


 ## <a name="PreReqs"></a> Pre Reqs: Executar terraform de preparação de ambiente, e coletar informações relevantes ao processo

 1. Faça login em sua conta na Cloud. [link](https://www.oracle.com/cloud/sign-in.html) 
 2. Execute o [Laboratório 2](../2%20-%20Using%20Terraform%20on%20OCI/Tutorial.md) deste workshop - *Execute apenas se você não o executou anteriormente*
 3. No canto direito superior, clique no icone de perfil, e clique em seu usuário

 ![](./IMG/001-LAB4.png)

 4.  No canto esquerdo inferior, clique em **Auth Tokens**, em seguida clique em **Gerar Token**

 ![](./IMG/002-LAB4.png)

 5. Dê uma descrição ao token, e clique em **Gerar Token**

 ![](./IMG/003-LAB4.png)

 6. **ATENÇÃO** - Copie o código gerado para um **bloco de notas**, se caso você perder esse código será necessario gera-lo novamente

 
 ![](./IMG/004-LAB4.png)


 - Durante todo este laboratório, utilizaremos este código quando for solicitada a informação de **Auth Token**


 7. No menu, no canto esquerdo superior acesse: Observabilidade & Gerenciamento > Application Performance > Administração

 
 ![](./IMG/005-LAB4.png)


 8.  No canto esquerdo inferior, em Escopo, valide se o compartimento correto está selecionado:

  
 ![](./IMG/006-LAB4.png)


 9. Selecione o Dominio listado: 
   
 ![](./IMG/007-LAB4.png)

 10. Copie as informações necessárias para o bloco de notas:

    - APM_ENDPOINT: Item 1 da imagem
    - APM_PVDATAKEY: Item 2 da imagem

![](./IMG/008-LAB4.png)

 11. Retorne a página de dominios

 ![](./IMG/009-LAB4.png)
 
 12. No canto esquerdo inferior, em Recursos clique em **Download APM Agent**

 ![](./IMG/010-LAB4.png)
 
 13. **Com o botão direito do mouse** clique no item listado, e selecione **Copiar Link**

 ![](./IMG/011-LAB4.png)

 - APM_AGENT_URL: Cole o link copiado no bloco de notas 

Com isso cumprimos todos os pré requisitos para o laboratório:

 ![](./IMG/012-LAB4.png)
 



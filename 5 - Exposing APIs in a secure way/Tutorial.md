Lab01 – API Gateway

1 – Acessar a contole do OCI;

2 – Clicar no botão de menu hamburguer -\&gt; Developer Services -\&gt; API Management;

![](img1.png)

3 – Selecione o compartimento que criamos anteriormente e clique no botão **Create Gateway:**

![](RackMultipart20220121-4-f2tmuv_html_2cc86aaf635e3c8a.png)

4 **–** Preenchao nome do Gateway estou utilizando o valor **apigtw** , selecione o tipo como **Public** e verifique que estamos utilizando o compartimento que criamos anteriormente no meu caso **FF\_DEV** :

![](RackMultipart20220121-4-f2tmuv_html_7dd21d1bc18da0d7.png)

5 – Nas opções de Network selecionar a VCN e a **subnet publica** que criamos anteriormente:

![](RackMultipart20220121-4-f2tmuv_html_cfbf3209efbdef8d.png)

6 – Clique em **Create Gateway** ;

7 – Agora com o nosso Gateway criado vamos configura-lo para expor a Function que criamos anteriormente;

![](RackMultipart20220121-4-f2tmuv_html_fc4868d0663f0ee4.png)

8 – Escolher a opção Deployment no menu do lado direito:

![](RackMultipart20220121-4-f2tmuv_html_a03073fa88e9b591.png)

9 – Clique em **Create Deployment** :

![](RackMultipart20220121-4-f2tmuv_html_71e11e2cf26d25ae.png)

10 – Selecione a opção **From Scratch** , preencha o nome ![](RackMultipart20220121-4-f2tmuv_html_9c6e277f00d986e.png)

11 – Siga para as próximas opções, preencher o **PATH PREFIX** estou utilizando o valor **/minhasfunctions** em seguinda garantir que o compartimento selecionado é o que criamos anteriormente **FF\_DEV** no meu caso:

![](RackMultipart20220121-4-f2tmuv_html_86f732bb15ee700c.png)

12 – Em **API Request Policies** , podemos alterar configurações como CORS, Authentication e Rate Limiting, não iremos alterar nada:

![](RackMultipart20220121-4-f2tmuv_html_eaf368c03d88e898.png)

![](RackMultipart20220121-4-f2tmuv_html_b483347a1d37aeb9.png)

13 – Em **API Logging Policies** selecione **Information:**

![](RackMultipart20220121-4-f2tmuv_html_91b668978f2ebc02.png)

14 – Clique em **Next;**

15 – Preencher o **PATH** estou utilizando o valor **/function** , em **METHODS** selecionar **POST** e **GET** , selecionar **Oracle Function** em **TYPE:**

![](RackMultipart20220121-4-f2tmuv_html_81ee4e4df7a8b47a.png)

16 – Selecionar o **APPLICATION** de Functions que criamos anteriormente no meu caso **faas\_app** e selecionar a function que criamos anteriormente:

![](RackMultipart20220121-4-f2tmuv_html_a31aac938a236b47.png)

17 – Clique em **Next** :

![](RackMultipart20220121-4-f2tmuv_html_3a2d58e81fda2c7e.png)

18 – Revise todas as opções que escolhemos e clique me **Create** :

![](RackMultipart20220121-4-f2tmuv_html_b3c9c9f4add8d43e.png)

19 – Aguardar a conclusão do deployment:

![](RackMultipart20220121-4-f2tmuv_html_cb9bcb9e0e99cf37.png)

20 – Testar o a exposição da nossa API utilizar o host do Gateway + PATH do depolyment e PATH da rota:

No meu caso: https://gun4muas3cq5mvdpcubazhozga.apigateway.sa-vinhedo-1.oci.customer-oci.com **/minhasfunctions/function**

![](RackMultipart20220121-4-f2tmuv_html_19f049acc724d8a2.png)

21 – O erro aconteceu porque não autorizamos o serviço **API Gateway** a chamar o serviço de **Functions**. Acessar o menu hamburguer -\&gt; **Identity &amp; Security** -\&gt; **Compartments** :

![](RackMultipart20220121-4-f2tmuv_html_f477a9e5562f0f96.png)

22 – Obter e anotar o OCID do compartimento que criamos para executar os labs, conforme o screenshot abaixo:

![](RackMultipart20220121-4-f2tmuv_html_6ca1e732a0eb344d.png)

21 – No menu do lado esquerdo acessar a opção **Dynamic Groups** :

![](RackMultipart20220121-4-f2tmuv_html_b409b422155fd5e8.png)

22 – Clique em **Create Dynamic Group;**

23 – Preencher o nome e descriçao, estou utilizando os valores:

| Name: | dg-apigtw |
| --- | --- |
| Description: | Dynamic Group for API Gateway |

![](RackMultipart20220121-4-f2tmuv_html_4b24fcbca81bbff4.png)

24 – Em Matching Rules vamos preencher com o seguinte valor não se esquece de colocar o OCID do compartimento que anotamos anteriormente:

| ALL {resource.type = &#39;ApiGateway&#39;, resource.compartment.id = &#39;ocid1.compartment.oc1..aaaaaaaaf6sqq62lqwehudicflh6d2z3cayq5srigegtujdqwgh5j2w445fq&#39;} |
| --- |

![](RackMultipart20220121-4-f2tmuv_html_31c0c9051002a54d.png)

25 – Em seguida clique no botão **Create** ;

26 – Com o nosso Dynamic Group criado vamos criar uma politica de acesso. Acessar o menu hamburguer -\&gt; **Identity &amp; Security** -\&gt; **Policies** ;

![](RackMultipart20220121-4-f2tmuv_html_f9dd4ec51d587117.png)

27 – Garanta que o compartment selecionado é o root, caso não estaja no root seleciona-lo no menu ao lado esquerdo em **List Scope** ;

28 - Clique no botão **Create Policy** , em seguida preencha **Name** e **Description** utilizei os valores abaixo:

| Name: | policy-apigtw |
| --- | --- |
| Description: | Policy for API Gateway |

![](RackMultipart20220121-4-f2tmuv_html_19a38f38905fb8a.png)

29 - Marque a opção **Show manual editor** e preencha o campo **Policy Builder** , não esqueça de mudar **[Nome do Dynamic Group]** e **[Nome do compartimento]**, para os valores que configuramos anteriormente:

| allow dynamic-group **[Nome do Dynamic Group]** to use virtual-network-family in compartment **[Nome do compartimento]**allow dynamic-group **[Nome do Dynamic Group]** to manage public-ips in compartment **[Nome do compartimento]**allow dynamic-group **[Nome do Dynamic Group]** to use functions-family in compartment **[Nome do compartimento]**allow any-user to use functions-family in compartment FF\_DEV |
| --- |

No meu caso ficou dessa maneira:

![](RackMultipart20220121-4-f2tmuv_html_2ce4152cf8567116.png)

30 – Clique em create;

31 – Testar a exposição da nossa API novamente, voce pode testar pelo Navegador, Terminal, Postman ou Cloud Shell:

![](RackMultipart20220121-4-f2tmuv_html_36dd864b3f7ecc14.png)

| curl -X POST https://gun4muas3cq5mvdpcubazhozga.apigateway.sa-vinhedo-1.oci.customer-oci.com/minhasfunctions/function -d &#39;{&quot;name&quot;:&quot;Vinicius&quot;}&#39;
curl -X GET https://gun4muas3cq5mvdpcubazhozga.apigateway.sa-vinhedo-1.oci.customer-oci.com/minhasfunctions/function |
| --- |

32 – Desafio criar mais uma rota no Deployment que criamos anteriormente utilizando um resposta pre definida.

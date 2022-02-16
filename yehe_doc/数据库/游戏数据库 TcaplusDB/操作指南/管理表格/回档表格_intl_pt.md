## Cenários de operação 
Este documento descreve como reverter registros especificados no console do TcaplusDB.

## Pré-requisitos
Você criou uma tabela. Para obter mais informações, consulte [Criação de tabela](https://intl.cloud.tencent.com/document/product/1016/32715).

## Instruções
1. Acesse a página [Lista de tabelas](https://console.cloud.tencent.com/tcaplusdb/table), selecione a tabela em questão e clique em **More (Mais)** > **Roll back (Reverter)** na coluna "Operation (Operação)", ou selecione várias tabelas e clique em **Batch Rollback (Reversão em lote)** na parte superior.
2. Na caixa de diálogo pop-up, carregue um arquivo .txt que contém os valores dos campos do registro em questão.
   O arquivo está no seguinte formato:
   Suponha que sua tabela seja definida da seguinte forma, em que as chaves principais são `openid`, `tconndid` e `timekey`:
```
syntax = "proto2";
package myTcaplusTable;
import "tcaplusservice.optionv1.proto";
message tb_online {
    option(tcaplusservice.tcaplus_primary_key) = "openid,tconndid,timekey";
    required int32 openid = 1; //QQ Uin
    required int32 tconndid = 2;
    required string timekey = 3;
    required string gamesvrid = 4;
	optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; 
	optional pay_info pay = 7;
	message pay_info {
		optional uint64 total_money = 1;
		optional uint64 pay_times = 2;
	}
}
```
Para reverter um registro com as chaves `openid` = 100, `tconndid`= 1 e `imekey` = '123456', você precisa preparar um arquivo contendo as chaves conforme abaixo. A primeira linha contém os nomes das chaves principais separadas por espaço, e a segunda linha e as subsequentes contêm os valores das chaves principais dos registros a serem revertidos.
```
openid tconndid timekey 
100 1 123456
```
4. Após o upload do arquivo key.txt, selecione o tempo de reversão e clique em **Submit (Enviar)**.
![](https://main.qcloudimg.com/raw/60f9532439c46ae11803a267bed79f98.png)


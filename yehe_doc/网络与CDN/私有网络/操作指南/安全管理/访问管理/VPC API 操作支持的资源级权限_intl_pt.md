Você pode autorizar as seguintes operações de API para recursos do VPC no CAM. Os recursos compatíveis com APIs específicas e as condições correspondentes são os seguintes:
>As operações de API do VPC fora da tabela não aceitam permissões no nível de recursos. Você ainda pode autorizar o usuário a executar essas operações, mas deve especificar `*` como o elemento de recurso na instrução da política.

<table border=3D0 cellpadding=3D0 cellspacing=3D0 width=3D504 style=3D'bord=
er-collapse:
 collapse;table-layout:fixed;width:378pt'>
 <col width=3D72 span=3D7 style=3D'width:54pt'>
 <tr height=3D18 style=3D'height:13.5pt'>
  <td height=3D18 width=3D72 style=3D'height:13.5pt;width:54pt'>Operação da API</t=
d>
  <td width=3D72 style=3D'width:54pt'>Recurso</td>
  <td width=3D72 style=3D'width:54pt'>Condição</td>
  <td width=3D72 style=3D'width:54pt'>Observações</td>
 </tr>
 <tr height=3D180 style=3D'height:135.0pt' >
  <td height=3D180 style=3D'height:135.0pt' >AcceptVp<span style=3D'display:=
none'>cPeeringConnection</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D324 style=3D'height:243.0pt'>
  <td height=3D324 style=3D'height:243.0pt' >—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:region<br>
    vpc:requester_vpc</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId (o vpcId do receptor)</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D432 style=3D'height:324.0pt'>
  <td height=3D432 style=3D'height:324.0pt'>AcceptVp<span style=3D'display:=
none'>cPeeringConnectionEx</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:accepter_vpc_region<br>
    vpc:requester_vpc<br>
    vpc:requester_vpc_region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:accepter_vpc_region` representa a região do receptor.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:requester_vpc_region` representa a região onde o iniciador está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>AddVpnCo<span style=3D'display:=
none'>nnEx</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPN Gateway<br>
    qcs::vpc:$region:$account:vpngw/*<br>
    qcs::vpc:$region:$account:vpngw/$vpnGwId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D108 style=3D'height:81.0pt'>
  <td height=3D108 style=3D'height:81.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do cliente<br>
    qcs::vpc:$region:$account:cgw/*</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D198 style=3D'height:148.5pt'>
  <td height=3D198 style=3D'height:148.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso túnel VPN<br>
    qcs::vpc:$region:$account:vpnx/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:vpngw<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:vpngw` representa o VPN Gateway do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>AssignPr<span style=3D'display:=
none'>ivateIpAddresses</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>Associat<span style=3D'display:=
none'>eVip</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>Associat<span style=3D'display:=
none'>eRouteTable</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso sub-rede<br>
    qcs::vpc:$region:$account:subnet/*<br>
    qcs::vpc:$region:$account:subnet/$subnetId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso tabela de rotas<br>
    qcs::vpc:$region:$account:rtb/*<br>
    qcs::vpc:$region:$account:rtb/$routeTableId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>AttachCl<span style=3D'display:=
none'>assicLinkVpc</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso CVM<br>
    qcs::cvm:$region:$account:instance/*<br>
    qcs::cvm:$region:$account:instance/$instanceId</td>
  <td>cvm:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D4 style=3D'mso-ignore:colspan'>`cvm:region` representa a região onde o CVM está localizado.</td>
 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>AttachNe<span style=3D'display:=
none'>tworkInterface</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso CVM<br>
    qcs::cvm:$region:$account:instance/*<br>
    qcs::cvm:$region:$account:instance/$instanceId</td>
  <td>cvm:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D4 style=3D'mso-ignore:colspan'>`cvm:region` rrepresenta a região onde o CVM está localizado
.</td>
 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>CreateAn<span style=3D'display:=
none'>dAttachNetworkInterface</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso CVM<br>
    qcs::cvm:$region:$account:instance/*<br>
    qcs::cvm:$region:$account:instance/$instanceId</td>
  <td>cvm:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D4 style=3D'mso-ignore:colspan'>`cvm:region` rrepresenta a região onde o CVM está localizado
.</td>
 </tr>
 <tr height=3D198 style=3D'height:148.5pt'>
  <td height=3D198 style=3D'height:148.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>CreateDi<span style=3D'display:=
none'>rectConnectGateway</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D126 style=3D'height:94.5pt'>
  <td height=3D126 style=3D'height:94.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>CreateLo<span style=3D'display:=
none'>calDestinationIPPortTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>CreateLo<span style=3D'display:=
none'>calIPTranslationAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>CreateLo<span style=3D'display:=
none'>calIPTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>CreateLo<span style=3D'display:=
none'>calSourceIPPortTranslationAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>CreateLo<span style=3D'display:=
none'>calSourceIPPortTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>CreatePe<span style=3D'display:=
none'>erIPTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>CreateNa<span style=3D'display:=
none'>tGateway</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D126 style=3D'height:94.5pt'>
  <td height=3D126 style=3D'height:94.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso NAT Gateway<br>
    qcs::vpc:$region:$account:nat/*<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>CreateNe<span style=3D'display:=
none'>tworkAcl</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D126 style=3D'height:94.5pt'>
  <td height=3D126 style=3D'height:94.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ACL de rede<br>
    qcs::vpc:$region:$account:acl/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>CreateNe<span style=3D'display:=
none'>tworkInterface</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso sub-rede<br>
    qcs::vpc:$region:$account:subnet/*<br>
    qcs::vpc:$region:$account:subnet/$subnetId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>CreateRo<span style=3D'display:=
none'>ute</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso tabela de rotas<br>
    qcs::vpc:$region:$account:rtb/*<br>
    qcs::vpc:$region:$account:rtb/$routeTableId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>CreateRo<span style=3D'display:=
none'>uteTable</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D126 style=3D'height:94.5pt'>
  <td height=3D126 style=3D'height:94.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso tabela de rotas<br>
    qcs::vpc:$region:$account:rtb/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>CreateSu<span style=3D'display:=
none'>bnet</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D126 style=3D'height:94.5pt'>
  <td height=3D126 style=3D'height:94.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway da sub-rede<br>
    qcs::vpc:$region:$account:subnet/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>CreateSu<span style=3D'display:=
none'>bnetAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ACL de rede<br>
    qcs::vpc:$region:$account:acl/*<br>
    qcs::vpc:$region:$account:acl/$networkAclId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D126 style=3D'height:94.5pt'>
  <td height=3D126 style=3D'height:94.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway da sub-rede<br>
    qcs::vpc:$region:$account:subnet/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D198 style=3D'height:148.5pt'>
  <td height=3D198 style=3D'height:148.5pt'>CreateVp<span style=3D'display:=
none'>cPeeringConnection</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC (iniciador)<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D324 style=3D'height:243.0pt'>
  <td height=3D324 style=3D'height:243.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:requester_vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>CreateVp<span style=3D'display:=
none'>cPeeringConnectionEx</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D432 style=3D'height:324.0pt'>
  <td height=3D432 style=3D'height:324.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:accepter_vpc_region<br>
    vpc:requester_vpc<br>
    vpc:requester_vpc_region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:accepter_vpc_region` representa a região onde o receptor está localizado.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:requester_vpc_region` representa a região onde o iniciador está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DeleteDi<span style=3D'display:=
none'>rectConnectGateway</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DeleteLo<span style=3D'display:=
none'>calDestinationIPPortTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DeleteLo<span style=3D'display:=
none'>calIPTranslationAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DeleteLo<span style=3D'display:=
none'>calIPTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DeleteLo<span style=3D'display:=
none'>calSourceIPPortTranslationAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DeletePe<span style=3D'display:=
none'>erIPTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DeleteLo<span style=3D'display:=
none'>calSourceIPPortTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>DeleteNa<span style=3D'display:=
none'>tGateway</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso NAT Gateway<br>
    qcs::vpc:$region:$account:nat/*<br>
    qcs::vpc:$region:$account:nat/$natId<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>DeleteNe<span style=3D'display:=
none'>tworkAcl</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ACL de rede<br>
    qcs::vpc:$region:$account:acl/*<br>
    qcs::vpc:$region:$account:acl/$networkAclId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DeleteNe<span style=3D'display:=
none'>tworkInterface</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>DeleteRo<span style=3D'display:=
none'>ute</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso tabela de rotas<br>
    qcs::vpc:$region:$account:rtb/*<br>
    qcs::vpc:$region:$account:rtb/$routeTableId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>DeleteRo<span style=3D'display:=
none'>uteTable</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso tabela de rotas<br>
    qcs::vpc:$region:$account:rtb/*<br>
    qcs::vpc:$region:$account:rtb/$routeTableId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>DeleteSu<span style=3D'display:=
none'>bnet</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso sub-rede<br>
    qcs::vpc:$region:$account:subnet/*<br>
    qcs::vpc:$region:$account:subnet/$subnetId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D198 style=3D'height:148.5pt'>
  <td height=3D198 style=3D'height:148.5pt'>DeleteUs<span style=3D'display:=
none'>erGw</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do cliente<br>
    qcs::vpc:$region:$account:cgw/*<br>
    qcs::vpc:$region:$account:cgw/$userGwId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>DeleteVpc</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:region<br>
    vpc:vpc<br>
    </td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D324 style=3D'height:243.0pt'>
  <td height=3D324 style=3D'height:243.0pt'>DeleteVp<span style=3D'display:=
none'>cPeeringConnection</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:region<br>
    vpc:requester_vpc<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D432 style=3D'height:324.0pt'>
  <td height=3D432 style=3D'height:324.0pt'>DeleteVp<span style=3D'display:=
none'>cPeeringConnectionEx</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:accepter_vpc_region<br>
    vpc:requester_vpc<br>
    vpc:requester_vpc_region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:accepter_vpc_region` representa a região onde o receptor está localizado.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:requester_vpc_region` representa a região onde o iniciador está localizado.</td>

 </tr>
 <tr height=3D270 style=3D'height:202.5pt'>
  <td height=3D270 style=3D'height:202.5pt'>DeleteVp<span style=3D'display:=
none'>nConn</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso túnel VPN<br>
    qcs::vpc:$region:$account:vpnx/*<br>
    qcs::vpc:$region:$account:vpnx/$vpnConnId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:vpngw<br>
    vpc:usergw<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:vpngw` representa o gateway do desenvolvedor.<br>
    `vpc:usergw` representa o gateway do cliente do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>DetachCl<span style=3D'display:=
none'>assicLinkVpc</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
    <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:region<br>
    vpc:vpc<br>
    </td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso CVM<br>
    qcs::cvm:$region:$account:instance/*<br>
    qcs::cvm:$region:$account:instance/$instanceId</td>
  <td>cvm:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D4 style=3D'mso-ignore:colspan'>`cvm:region` rrepresenta a região onde o CVM está localizado
.</td>
 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>DetachNe<span style=3D'display:=
none'>tworkInterface</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso CVM<br>
    qcs::cvm:$region:$account:instance/*<br>
    qcs::cvm:$region:$account:instance/$instanceId</td>
  <td>cvm:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D4 style=3D'mso-ignore:colspan'>`cvm:region` rrepresenta a região onde o CVM está localizado
.</td>
 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>DeteleSu<span style=3D'display:=
none'>bnetAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso sub-rede<br>
    qcs::vpc:$region:$account:subnet/*<br>
    qcs::vpc:$region:$account:subnet/$subnetId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ACL de rede<br>
    qcs::vpc:$region:$account:acl/*<br>
    qcs::vpc:$region:$account:acl/$networkAclId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>EipBindN<span style=3D'display:=
none'>atGateway</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso NAT Gateway<br>
    qcs::vpc:$region:$account:nat/*<br>
    qcs::vpc:$region:$account:nat/$natId<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>EipUnBin<span style=3D'display:=
none'>dNatGateway</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso NAT Gateway<br>
    qcs::vpc:$region:$account:nat/*<br>
    qcs::vpc:$region:$account:nat/$natId<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>EnableVp<span style=3D'display:=
none'>cPeeringConnection</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D324 style=3D'height:243.0pt'>
  <td height=3D324 style=3D'height:243.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:region<br>
    vpc:requester_vpc<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>EnableVp<span style=3D'display:=
none'>cPeeringConnectionEx</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D432 style=3D'height:324.0pt'>
  <td height=3D432 style=3D'height:324.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:accepter_vpc_region<br>
    vpc:requester_vpc<br>
    vpc:requester_vpc_region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:accepter_vpc_region` representa a região onde o receptor está localizado.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:requester_vpc_region` representa a região onde o iniciador está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>MigrateN<span style=3D'display:=
none'>etworkInterface</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D288 style=3D'height:216.0pt'>
  <td height=3D288 style=3D'height:216.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso CVM<br>
    qcs::cvm:$region:$account:instance/*<br>
    qcs::cvm:$region:$account:instance/$instanceId(a autorização é necessária antes e depois da migração)</t=
d>
  <td>cvm:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D4 style=3D'mso-ignore:colspan'>`cvm:region` rrepresenta a região onde o CVM está localizado
.</td>
 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>MigrateP<span style=3D'display:=
none'>rivateIpAddress</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyDi<span style=3D'display:=
none'>rectConnectGateway</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyLo<span style=3D'display:=
none'>calDestinationIPPortTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyLo<span style=3D'display:=
none'>calIPTranslationAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyLo<span style=3D'display:=
none'>calIPTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyLo<span style=3D'display:=
none'>calSourceIPPortTranslationAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyPe<span style=3D'display:=
none'>erIPTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyLo<span style=3D'display:=
none'>calSourceIPPortTranslationNatRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>ModifyNa<span style=3D'display:=
none'>tGateway</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso NAT Gateway<br>
    qcs::vpc:$region:$account:nat/*<br>
    qcs::vpc:$region:$account:nat/nat-dc7cdf<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>ModifyNe<span style=3D'display:=
none'>tworkAcl</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ACL de rede<br>
    qcs::vpc:$region:$account:acl/*<br>
    qcs::vpc:$region:$account:acl/$networkAclId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>ModifyNe<span style=3D'display:=
none'>tworkAclEntry</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ACL de rede<br>
    qcs::vpc:$region:$account:acl/*<br>
    qcs::vpc:$region:$account:acl/$networkAclId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyNe<span style=3D'display:=
none'>tworkInterface</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>ModifyPr<span style=3D'display:=
none'>ivateIpAddress</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc representa o VPC do desenvolvedor.<b=
r>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>ModifyRo<span style=3D'display:=
none'>uteTableAttribute</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso tabela de rotas<br>
    qcs::vpc:$region:$account:rtb/*<br>
    qcs::vpc:$region:$account:rtb/$routeTableId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>ModifySu<span style=3D'display:=
none'>bnetAttribute</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso sub-rede<br>
    qcs::vpc:$region:$account:subnet/*<br>
    qcs::vpc:$region:$account:subnet/$subnetId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D198 style=3D'height:148.5pt'>
  <td height=3D198 style=3D'height:148.5pt'>ModifyUs<span style=3D'display:=
none'>erGw</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do cliente<br>
    qcs::vpc:$region:$account:cgw/*<br>
    qcs::vpc:$region:$account:cgw/$userGwId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>ModifyVp<span style=3D'display:=
none'>cAttribute</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:Regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>ModifyVp<span style=3D'display:=
none'>cPeeringConnection</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D324 style=3D'height:243.0pt'>
  <td height=3D324 style=3D'height:243.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:region<br>
    vpc:requester_vpc<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>ModifyVp<span style=3D'display:=
none'>cPeeringConnectionEx</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D432 style=3D'height:324.0pt'>
  <td height=3D432 style=3D'height:324.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:accepter_vpc_region<br>
    vpc:requester_vpc<br>
    vpc:requester_vpc_region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:accepter_vpc_region` representa a região onde o receptor está localizado.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:requester_vpc_region` representa a região onde o iniciador está localizado.</td>

 </tr>
 <tr height=3D270 style=3D'height:202.5pt'>
  <td height=3D270 style=3D'height:202.5pt'>ModifyVp<span style=3D'display:=
none'>nConnEx</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso túnel VPN<br>
    qcs::vpc:$region:$account:vpnx/*<br>
    qcs::vpc:$region:$account:vpnx/$vpnConnId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:vpngw<br>
    vpc:usergw<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:vpngw` representa o gateway do desenvolvedor.<br>
    `vpc:usergw` representa o gateway do cliente do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>ModifyVp<span style=3D'display:=
none'>nGw</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPN Gateway<br>
    qcs::vpc:$region:$account:vpngw/*<br>
    qcs::vpc:$region:$account:vpngw/$vpnGwId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>RejectVp<span style=3D'display:=
none'>cPeeringConnection</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D324 style=3D'height:243.0pt'>
  <td height=3D324 style=3D'height:243.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:region<br>
    vpc:requester_vpc<br>
    </td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D180 style=3D'height:135.0pt'>
  <td height=3D180 style=3D'height:135.0pt'>RejectVp<span style=3D'display:=
none'>cPeeringConnectionEx</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPC<br>
    qcs::vpc:$region:$account:vpc/*<br>
    qcs::vpc:$region:$account:vpc/$vpcId</td>
  <td>vpc:regi<span style=3D'display:none'>on</span></td>
  <td colspan=3D3 style=3D'mso-ignore:colspan'>`vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
 <tr height=3D432 style=3D'height:324.0pt'>
  <td height=3D432 style=3D'height:324.0pt'>—</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso Peering Connection<br>
    qcs::vpc:$region:$account:pcx/*<br>
    qcs::vpc:$region:$account:pcx/$peeringConnectionId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:accepter_vpc<br>
    vpc:accepter_vpc_region<br>
    vpc:requester_vpc<br>
    vpc:requester_vpc_region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:accepter_vpc` representa o VPC do receptor. O valor é o VPC do receptor.<br>
    `vpc:accepter_vpc_region` representa a região onde o receptor está localizado.<br>
    `vpc:requester_vpc` representa o VPC do iniciador. O valor é o VPC do iniciador.<br>
    `vpc:requester_vpc_region` representa a região onde o iniciador está localizado.</td>

 </tr>
 <tr height=3D270 style=3D'height:202.5pt'>
  <td height=3D270 style=3D'height:202.5pt'>ResetVpn<span style=3D'display:=
none'>ConnSA</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso túnel VPN<br>
    qcs::vpc:$region:$account:vpnx/*<br>
    qcs::vpc:$region:$account:vpnx/$vpnConnId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:vpngw<br>
    vpc:usergw<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:vpngw` representa o gateway do desenvolvedor.<br>
    `vpc:usergw` representa o gateway do cliente do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>SetLocal<span style=3D'display:=
none'>IPTranslationAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>SetLocal<span style=3D'display:=
none'>SourceIPPortTranslationAclRule</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso gateway do Direct Connect<br>
    qcs::vpc:$region:$account:dcg/*<br>
    qcs::vpc:$region:$account:dcg/$directConnectGatewayId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D216 style=3D'height:162.0pt'>
  <td height=3D216 style=3D'height:162.0pt'>SetSSLVp<span style=3D'display:=
none'>nDomain</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso VPN Gateway<br>
    qcs::vpc:$region:$account:vpngw/*<br>
    qcs::vpc:$region:$account:vpngw/$vpnGwId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>

 </tr>
 <tr height=3D234 style=3D'height:175.5pt'>
  <td height=3D234 style=3D'height:175.5pt'>Unassign<span style=3D'display:=
none'>PrivateIpAddresses</span></td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>Recurso ENI<br>
    qcs::vpc:$region:$account:eni/*<br>
    qcs::vpc:$region:$account:eni/$networkInterfaceId</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>vpc:vpc<br>
    vpc:subnet<br>
    vpc:region</td>
  <td class=3Dxl65 width=3D72 style=3D'width:54pt'>`vpc:vpc` representa o VPC do desenvolvedor.<br>
    `vpc:subnet` representa a sub-rede do desenvolvedor.<br>
    `vpc:region` representa a região onde o VPC está localizado.</td>
 </tr>
</table>


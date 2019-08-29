You can authorize the following API operations for key master resources in CAM. Below shows the resources supported by specific APIs and the corresponding conditions:

<table>
   <tr>
      <th>API Operation</th>
      <th>Resource</th>
      <th>Remarks</th>
   </tr>
   <tr>
      <td>kms:CreateKey</td>
      <td>qcs::kms:$region:$account:key/*</td>
      <td rowspan="23">creatorUin represents the UIN of the resource creator that can be a root account or sub-account.</td>
   </tr>
   <tr>
      <td>kms:ListKey</td>
      <td>qcs::kms:$region:$account:key/*</td>
   </tr>
   <tr>
      <td>kms:ListKeys</td>
      <td>qcs::kms:$region:$account:key/*</td>
   </tr>
   <tr>
      <td>kms:ListKeyDetail</td>
      <td>qcs::kms:$region:$account:key/*</td>
   </tr>
   <tr>
      <td>kms:GetServiceStatus</td>
      <td>qcs::kms:$region:$account:key/*</td>
   </tr>
   <tr>
      <td>kms:Encrypt</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:Decrypt</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms::GenerateDataKey</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms::EnableKey</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms::DisableKey</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms::GetKeyAttributes</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms::SetKeyAttributes</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:GetKeyRotationStatus</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:ReEncrypt</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:DescribeKey</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:UpdateKeyDescription</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:UpdateAlias</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:DisableKeyRotation</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:EnableKeyRotation</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:EnableKeys</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:DisableKeys</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
   <tr>
      <td>kms:DescribeKeys</td>
      <td>qcs::kms:$region:$account:key/creatorUin/$creatorUin/$keyid (authorizing one single resource) qcs::kms:$region:$account:key/creatorUin/$creatorUin/* (authorizing all resources of a specified creator) qcs::kms:$region:$account:key/* (authorizing all resources of a specified root account)</td>
   </tr>
</table>

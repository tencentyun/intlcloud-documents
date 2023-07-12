## Overview

CI's face recognition feature is a service kit that can verify the authenticity of user face information. It provides various verification modules, such as ID card OCR recognition and FaceID, to satisfy diverse user identity verification needs in different industries, including public security, human resources, social security, finance, and insurance.


<table>
<thead>
<tr>
<th width=20%>Feature</th>
<th width=80%>Description</th>
</tr>
</thead>
<tbody><tr>
<td>ID card OCR recognition</td>
<td><ul  style="margin: 0;"><li>This feature can recognize all fields on the front and back of a second-generation Chinese ID card, including name, gender, ethnicity, date of birth, address, ID number, issuing authority, and validity period. </li><li>It can also crop ID card photos and face photos, as well as warn about photographed, doctored, and photocopied images, edge and frame occlusions, temporary ID cards, and invalid validity periods.</li></ul></td>
</tr>
<tr>
<td>FaceID</td>
<td><ul  style="margin: 0;"><li>This feature integrates the capability of liveness detection and comparison with authoritative face libraries, where a selfie video, name, and ID card number can be passed in to verify the user's identity. </li><li>It first checks whether the face in the selfie video is a real person so as to prevent various types of attacks such as photo, video, and static 3D modeling.</li><li>After the liveness detection is completed, it further compares the face in the video with the face photo registered in an authoritative face library to determine whether they are the same person.</li></ul></td>


</tbody></table>

## Use Cases

#### Government affairs and public services
**Typical scenarios: Integrated government service, police service through WeChat Mini Program, business registration, and pensioner liveness verification**
FaceID supports user face recognition required for online business transaction processing with government agencies. Users can launch the WeChat official accounts, mini programs, or applications of government agencies, call FaceID for identity verification, and make appointments for various business transactions once verified.

#### Finance
**Typical scenarios: Bank account opening and insurance verification**
ID card recognition can be widely used in industries such as banking and securities where users' identities require verification to process business transactions such as remote account opening and large amount transfer, helping reduce banks' labor costs and improve the user convenience.
Commercial insurance companies and social security institutions are often unable to verify the identities and existences of beneficiaries as they may not come on site to complete the formalities in person for various reasons, including age and health conditions. With the FaceID service, those organizations can effectively avoid risks, such as insurance fraud.

#### ISP
**Typical scenarios: Services provided by ISPs, such as online mobile number application, SIM card purchase, and broadband service application**
The Ministry of Industry and Information Technology (MIIT) of China stipulates that users must verify their identities before they can use services provided by ISPs. Users can log in to the applications or WeChat official accounts of ISPs, verify their identities through FaceID, and activate and request mobile services online in a self-service manner.

#### Identity registration
**Typical scenarios: Internet access in internet cafés and hotel check-in**
Pursuant to applicable laws and regulations, identity registration is required in places such as internet cafés. In this case, the receptionist can call the FaceID service to verify user identities and register them before granting the internet access.

#### Transportation and mobility
**Typical scenarios: Passenger screening and boarding at airports, security check and ticket purchase at railway stations, ticket purchase at long-distance bus services, and border inspection and customs clearance**
Passengers may forget to carry their ID cards, so they cannot check in at airports. FaceID helps the public security administration build a temporary identity verification service on WeChat Mini Program. After passengers call the FaceID service on the mini program to verify their identities, temporary QR codes for boarding will be generated, which can be scanned for identity verification at check-in counters and boarding gates.

## Directions

Currently, you can call APIs to use the FaceID service. For more information, see FaceID).

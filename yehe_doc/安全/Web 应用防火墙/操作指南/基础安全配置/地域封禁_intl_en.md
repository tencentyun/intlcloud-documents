## Overview
You can add regions to the blocklist to block all access sources from the specific regions.

## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-baseconfig) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, select the target domain name in the top-left corner and click **Access control**.
3. On the access control page, click **Edit** next to the region being blocked.
![](https://qcloudimg.tencent-cloud.cn/raw/21b3e9a313eb5aac9fb9f2a376a967b2.png)
4. In the pop-up window, select the target region and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/ce7ba8a46c4fb04897e5a33d6e5681bc.png)
5. After saving the change, click ![](https://qcloudimg.tencent-cloud.cn/raw/690e27c541704c3f37923e41d22be586.png) in **Region blocked** to enable region blocking.
![](https://qcloudimg.tencent-cloud.cn/raw/b25eecdb30c28b0a4105e80cae12a55f.png)
6. Now you will be unable to visit your website from any of the blocked regions. For example, if you block all foreign regions, and visit a WAF-protected website with an overseas IP address, WAF will notify you that you have been blocked with an error page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ec257a0566e730d0028c19c611b40fed.png)

## Supported Regions
The following regions are supported:

#### China
| Region       | Province/City/Autonomous Region                                      |
| ---------- | ------------------------------------------ |
| East China   | Shandong, Jiangsu, Anhui, Zhejiang, Fujian, Jiangxi, Shanghai |
| South China   | Guangdong, Guangxi, Hainan                         |
| Central China   | Hubei, Hunan and Henan                         |
| North China   | Beijing, Tianjin, Hebei, Shanxi, Inner Mongolia           |
| Northwest China   | Ningxia, Xinjiang, Qinghai, Shaanxi, Gansu             |
| Southwest China   | Sichuan, Yunnan, Guizhou, Tibet, Chongqing             |
| Northeast China   | Liaoning, Jilin, Heilongjiang                       |
| Hong Kong, Macao and Taiwan | Hong Kong, Macao and Taiwan                         |

#### Other countries and regions
| Continent   | Country/Region                                                    |
| ------ | ------------------------------------------------------------ |
| Asia | Azerbaijan, Armenia, Afghanistan, Bangladesh, Bahrain, Brunei, Bhutan, Cyprus, Cambodia, Timor-Leste, Georgia, Guernsey, India, Indonesia, Iran, Israel, Iraq, Japan, Jordan, Kazakhstan, Kuwait, Kyrgyzstan, Lebanon, Laos, Morocco, Mongolia, Myanmar, Maldives, Oman, Nepal, Palestine, Pakistan, Philippines, South Korea, Qatar, Sri Lanka, Syria, Saudi Arabia, Singapore, Thailand, Türkiye, Tajikistan, Turkmenistan, United Arab Emirates, Uzbekistan, Vietnam, Yemen, North Korea |
| Europe | Austria, Albania, Andorra, Belgium, Bulgaria, Belarus, Bosnia and Herzegovina, Czech Republic, Croatia, Denmark, Estonia, France, Finland, Faroe Islands, Germany, Greece, Gibraltar, Hungary, Italy, Ireland, Iceland, Isle of Man, Jersey, Lithuania, Latvia, Luxembourg, Liechtenstein, Moldova, Macedonia, the Republic of Malta, Montenegro, Monaco, Netherlands, Norway, Portugal, Poland, Switzerland, Sweden, Spain, Romania, Russia, Serbia, Slovenia, Slovakia, San Marino, United Kingdom, Ukraine, Vatican City |
| Africa | Algeria, Angola, Burkina Faso, Benin, Botswana, Burundi, Côte d'Ivoire, Cameroon, Democratic Republic of the Congo, Republic of the Congo, Cape Verde, Chad, Central Africa, Comoros, Djibouti, Egypt, Ecuador, Ethiopia, Equatorial Guinea, Ghana, Gabon, Gambia, Guinea, Guinea-Bissau, Kenya, Libya, Lesotho, Liberia, Morocco, Mauritius, Malawi, Mozambique, Madagascar, Mali, Mauritania, Niger, Namibia, Nigeria, South Africa, Rwanda, Reunion, Sudan, Seychelles, Somalia, Swaziland, Sierra Leone, Senegal, Sao Tome and Principe, South Sudan, Tunisia, Tanzania, Togo, Uganda, Zambia, Zimbabwe |
| Oceania | Australia, American Samoa, Cook Islands, Fiji Islands, French Polynesia, Guam, Federated States of Micronesia, New Zealand, Nauru, Mariana Islands, New Caledonia, Papua New Guinea, Palau, Saint Lucia, Samoa, Solomon Islands, Tonga, Tuvalu, Vanuatu |
| North America | Antigua and Barbuda, Anguilla, Barbados, Belize, Bahamas, Bermuda, Canada, Costa Rica, Cuba, Cayman Islands, Caribbean Netherlands, Dominica, El Salvador, Guatemala, Greenland, Guadero Puerto Rico, Grenada, Honduras, Haiti, Jamaica, Mexico, Martinique, Nicaragua, Puerto Rico, Panama, Saint Martin, Saint Vincent and the Grenadines, Saint Martin, Saint Kitts and Nevis, Trini Da and Tobago, Tajikistan, English Virgin Islands, Dominica, Turks and Caicos Islands, United States, United States Virgin Islands |
| South America | Argentina, Aruba, Brazil, Bolivia, Colombia, Chile, Curacao, French Guiana, Guyana, Paraguay, Peru, Suriname, Uruguay, Venezuela |




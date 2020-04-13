# Table of Contents

* [Python DateTime, TimeDelta, Strftime\(Format\) with Examples](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#python-datetime-timedelta-strftime-format-with-examples)
* [How to Use Date & DateTime Class](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#how-to-use-date-datetime-class)
* [Print Date using date.today\(\)](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#print-date-using-date-today)
  * [Today’s Weekday Number](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#today-s-weekday-number)
* [Python Current Date and Time: now\(\) today\(\)](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#python-current-date-and-time-now-today)
* [How to Format Date and Time Output with Strftime\(\)](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#how-to-format-date-and-time-output-with-strftime)
* [How to use Timedelta Objects](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#how-to-use-timedelta-objects)
* [Python 2 Example](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#python-2-example)
  * [Summary](http://localhost:1313/library/tutorials/docs/python/beginer/date-and-time/datetime-timedelta-strftime/#summary)

\| NO. \| รหัสประเทศ \|ชื่อประเทศ \|สกุลเงิน \|

\|:------:\|:-------:\|---------\|-----\|

\| 1 \|AD \|ANDORRA \|AUD \|

\| 2 \|AE \|UNITED ARAB EMIRATES \|THB \|

\| 3 \|AF \|AFGHANISTAN \|BEF \|

\| 4 \|AG \|ANTIGUA AND BARBUDA \|BND \|

\| 5 \|AL \|ALBANIA \|CAD \|

\| 6 \|AM \|ARMENIA \|DKK \|

\| 7 \|AN \|NETHERLANDS ANTILLES \|DEM \|

\| 8 \|AO \|ANGOLA \|VND \|

\| 9 \|AR \|ARGENTINA \|EUR \|

\| 10 \|AS \|AMERICAN SAMOA \|RFR \|

\| 11 \|AT \|AUSTRIA \|HKD \|

\| 12 \|AU \|AUSTRALIA \|INR \|

\| 13 \|AW \|ARUBA \|IEP \|

\| 14 \|AZ \|AZERBAIJAN \|ITL \|

\| 15 \|BB \|BARBADOS \|JOD \|

\| 16 \|BD \|BANGLADESH \|LAK \|

\| 17 \|BE \|BELGIUM \|KWD \|

\| 18 \|BF \|BURKINA FASO \|MMK \|

\| 19 \|BG \|BULGARIA \|MYR \|

\| 20 \|BH \|BAHRAIN \|MTL \|

\| 21 \|BI \|BURUNDI \|FIM \|

\| 22 \|BJ \|BENIN \|MXN \|

\| 23 \|BM \|BERMUDA \|NLG \|

\| 24 \|BN \|BRUNEI DARUSSALAM \|TWD \|

\| 25 \|BO \|BOLIVIA \|NZD \|

\| 26 \|BR \|BRAZIL \|NOK \|

\| 27 \|BS \|BAHAMAS \|PKR \|

\| 28 \|BT \|BHUTAN \|PHP \|

\| 29 \|BV \|BOUVET ISLAND \|PTE \|

\| 30 \|BW \|BOTSWANA \|GBP \|

\| 31 \|BY \|BELARUS \|ZAR \|

\| 32 \|BZ \|BELIZE \|KHR \|

\| 33 \|CA \|CANADA \|IDR \|

\| 34 \|CC \|COCOS \(KEELING\) IS.S \|SAR \|

\| 35 \|CF \|CENTRAL AFRICAN REP. \|ATS \|

\| 36 \|CG \|CONGO \|SGD \|

\| 37 \|CH \|SWITZERLAND \|ESP \|

\| 38 \|CI \|COTE D IVOIRE \|SEK \|

\| 39 \|CK \|COOK ISLANDS \|CHF \|

\| 40 \|CL \|CHILE \|BDT \|

\| 41 \|CM \|CAMEROON \|AED \|

\| 42 \|CN \|CHINA \|USD \|

\| 43 \|CO \|COLOMBIA \|KRW \|

\| 44 \|CR \|COSTA RICA \|JPY \|

\| 45 \|CU \|CUBA \|CNY \|

\| 46 \|CV \|CAPE VERDE \| \|

\| 47 \|CX \|CHRISTMAS ISLAND \| \|

\| 48 \|CY \|CYPRUS \| \|

\| 49 \|CZ \|CZECH REPUBLIC \| \|

\| 50 \|DE \|GERMANY \| \|

\| 51 \|DJ \|DJIBOUTI \| \|

\| 52 \|DK \|DENMARK \| \|

\| 53 \|DM \|DOMINICA \| \|

\| 54 \|DO \|DOMINICAN REPUBLIC \| \|

\| 55 \|DZ \|ALGERIA \| \|

\| 56 \|EC \|ECUADOR \| \|

\| 57 \|EE \|ESTONIA \| \|

\| 58 \|EG \|EGYPT \| \|

\| 59 \|EH \|WESTERN SAHARA \| \|

\| 60 \|ER \|ERITREA \| \|

\| 61 \|ES \|SPAIN \| \|

\| 62 \|ET \|ETHIOPIA \| \|

\| 63 \|FI \|FINLAND \| \|

\| 64 \|FJ \|FIJI \| \|

\| 65 \|FK \|FALKLAND ISLANDS \(MALVINAS\) \| \|

\| 66 \|FM \|MICRONESIA \(FEDERATED STATES OF\) \| \|

\| 67 \|FO \|FAROE ISLANDS \| \|

\| 68 \|FR \|FRANCE \| \|

\| 69 \|FX \|FRANCE, METROPOLITAN \| \|

\| 70 \|GA \|GABON \| \|

\| 71 \|GB \|UNITED KINGDOM \| \|

\| 72 \|GD \|GRENADA \| \|

\| 73 \|GE \|GEORGIA \| \|

\| 74 \|GF \|FRENCE GUIANA \| \|

\| 75 \|GH \|GHANA \| \|

\| 76 \|GI \|GIBRALTAR \| \|

\| 77 \|GL \|GREENLAND \| \|

\| 78 \|GM \|GAMBIA \| \|

\| 79 \|GN \|GUINEA \| \|

\| 80 \|GP \|GUADELOUPE \| \|

\| 81 \|GQ \|EQUATORIAL GUINEA \| \|

\| 82 \|GR \|GREECE \| \|

\| 83 \|GS \|SOUTH \| \|

\| 84 \|GT \|GUATEMALA \| \|

\| 85 \|GU \|GUAM \| \|

\| 86 \|GW \|GUINEA-BISSAU \| \|

\| 87 \|GY \|GUYANA \| \|

\| 88 \|HK \|HONG KONG \| \|

\| 89 \|HM \|HEARD ISLAND AND MCDONALD ISLANDS \| \|

\| 90 \|HN \|HONDURAS \| \|

\| 91 \|HR \|CROATIA \| \|

\| 92 \|HT \|HAITI \| \|

\| 93 \|HU \|HUNGARY \| \|

\| 94 \|ID \|INDONESIA \| \|

\| 95 \|IE \|IRELAND \| \|

\| 96 \|IL \|ISRAEL \| \|

\| 97 \|IN \|INDIA \| \|

\| 98 \|IO \|BRITISH INDIAN OCEAN TERRITORY \| \|

\| 99 \|IQ \|IRAQ \| \|

\| 100 \|IR \|IRAN \| \|

\| 101 \|IS \|ICELAND \| \|

\| 102 \|IT \|ITALY \| \|

\| 103 \|JM \|JAMAICA \| \|

\| 104 \|JO \|JORDAN \| \|

\| 105 \|JP \|JAPAN \| \|

\| 106 \|KE \|KENYA \| \|

\| 107 \|KG \|KYRGYZSTAN \| \|

\| 108 \|KH \|CAMBODIA \| \|

\| 109 \|KI \|KIRIBATI \| \|

\| 110 \|KM \|COMOROS \| \|

\| 111 \|KN \|SAINT KITTS AND NEVIS \| \|

\| 112 \|KP \|KOREA \| \|

\| 113 \|KR \|KOREA,REPUBLIC OF \| \|

\| 114 \|KW \|KUWAIT \| \|

\| 115 \|KY \|CAYMAN ISLANDS \| \|

\| 116 \|KZ \|KAZAKHSTAN \| \|

\| 117 \|LA \|LAO REPUBLIC \| \|

\| 118 \|LB \|LEBANON \| \|

\| 119 \|LC \|SAINT LUCIA \| \|

\| 120 \|LI \|LIECHTENSTEIN \| \|

\| 121 \|LK \|SRI LANKA \| \|

\| 122 \|LR \|LIBERIA \| \|

\| 123 \|LS \|LESOTHO \| \|

\| 124 \|LT \|LITHUANIA \| \|

\| 125 \|LU \|LUXEMBOURG \| \|

\| 126 \|LV \|LATVIA \| \|

\| 127 \|LY \|LIBYAN ARAB JAMAHIRIYA \| \|

\| 128 \|MA \|MOROCCO \| \|

\| 129 \|MC \|MONACO \| \|

\| 130 \|MD \|MOLDOVA REPUBLIC OF \| \|

\| 131 \|MG \|MADAGASCAR \| \|

\| 132 \|MH \|MARSHALL ISLAND \| \|

\| 133 \|MK \|MACEDONIA \| \|

\| 134 \|ML \|MALI \| \|

\| 135 \|MM \|MYANMAR \| \|

\| 136 \|MN \|MONGOLIA \| \|

\| 137 \|MO \|MACAU \| \|

\| 138 \|MP \|NORTHERN MARIANA ISLANDS \| \|

\| 139 \|MQ \|MARTINIQUE \| \|

\| 140 \|MR \|MAURITANIA \| \|

\| 141 \|MS \|MONTSERRAT \| \|

\| 142 \|MT \|MALTA \| \|

\| 143 \|MU \|MAURITIUS \| \|

\| 144 \|MV \|MALDIVES \| \|

\| 145 \|MW \|MALAWI \| \|

\| 146 \|MX \|MEXICO \| \|

\| 147 \|MY \|MALAYSIA \| \|

\| 148 \|MZ \|MOZAMBIQUE \| \|

\| 149 \|NA \|NAMIBIA \| \|

\| 150 \|NC \|NEW CALEDONIA \| \|

\| 151 \|NE \|NIGER \| \|

\| 152 \|NF \|NORFOLK ISLAND \| \|

\| 153 \|NG \|NIGERIA \| \|

\| 154 \|NI \|NICARAGUA \| \|

\| 155 \|NL \|NETHERLANDS \| \|

\| 156 \|NO \|NORWAY \| \|

\| 157 \|NP \|NEPAL \| \|

\| 158 \|NR \|NAURU \| \|

\| 159 \|NU \|NIUE \| \|

\| 160 \|NZ \|NEW ZEALAND \| \|

\| 161 \|OM \|OMAN \| \|

\| 162 \|OT \|OTHER COUNTRY \| \|

\| 163 \|PA \|PANAMA \| \|

\| 164 \|PE \|PERU \| \|

\| 165 \|PF \|FRENCH POLYNESIA \| \|

\| 166 \|PG \|PAPUA NEW GUINEA \| \|

\| 167 \|PH \|PHILIPPINES \| \|

\| 168 \|PK \|PAKISTAN \| \|

\| 169 \|PL \|POLAND \| \|

\| 170 \|PM \|SAINT PIERRE AND MIQUELON \| \|

\| 171 \|PN \|PITCAIRN \| \|

\| 172 \|PR \|PUERTO RICO \| \|

\| 173 \|PT \|PORTUGAL \| \|

\| 174 \|PW \|PALAU \| \|

\| 175 \|PY \|PARAGUAY \| \|

\| 176 \|QA \|QATAR \| \|

\| 177 \|RE \|REUNION \| \|

\| 178 \|RO \|ROMANIA \| \|

\| 179 \|RU \|RUSSIAN FEDERATION \| \|

\| 180 \|RW \|RWANDA \| \|

\| 181 \|SA \|SAUDI ARABIA \| \|

\| 182 \|SB \|SOLOMON ISLANDS \| \|

\| 183 \|SC \|SEYCHELLES \| \|

\| 184 \|SD \|SUDAN \| \|

\| 185 \|SE \|SWEDEN \| \|

\| 186 \|SG \|SINGAPORE \| \|

\| 187 \|SH \|SAINT HELENA \| \|

\| 188 \|SI \|SLOVENIA \| \|

\| 189 \|SJ \|SVALBARD AND JAN MAYEN \| \|

\| 190 \|SK \|SLOVAKIA \| \|

\| 191 \|SL \|SIERRA LEONE \| \|

\| 192 \|SM \|SAN MARINO \| \|

\| 193 \|SN \|SENEGAL \| \|

\| 194 \|SO \|SOMALIA \| \|

\| 195 \|SR \|SURINAME \| \|

\| 196 \|ST \|SAO TOME AND PRINCIPE \| \|

\| 197 \|SV \|EL SALVADOR \| \|

\| 198 \|SY \|SYRIAN ARAB REPUBLIC \| \|

\| 199 \|SZ \|SWAZILAND \| \|

\| 200 \|TC \|TURKS AND CAICOS ISLANDS \| \|

\| 201 \|TD \|CHAD \| \|

\| 202 \|TF \|FRENCH SOUTHERN TERRITORIES \| \|

\| 203 \|TG \|TOGO \| \|

\| 204 \|TH \|THAILAND \| \|

\| 205 \|TJ \|TAJIKISTAN \| \|

\| 206 \|TK \|TOKELAU \| \|

\| 207 \|TM \|TURKMENISTAN \| \|

\| 208 \|TN \|TUNISIA \| \|

\| 209 \|TO \|TONGA \| \|

\| 210 \|TP \|EAST TIMOR \| \|

\| 211 \|TR \|TURKEY \| \|

\| 212 \|TT \|TRINIDAD AND TOBAGO \| \|

\| 213 \|TV \|TUVALU \| \|

\| 214 \|TW \|TAIWAN PROVINCE OF CHINA \| \|

\| 215 \|TZ \|TANZANIA UNITED REPUBLIC OF \| \|

\| 216 \|UA \|UKRAINE \| \|

\| 217 \|UG \|UGANDA \| \|

\| 218 \|UM \|UNITED STATES MINOR \| \|

\| 219 \|US \|UNITED STATES \| \|

\| 220 \|UY \|URUGUAY \| \|

\| 221 \|UZ \|UZBEKISTAN \| \|

\| 222 \|VA \|VATICAN CITY \| \|

\| 223 \|VC \|SAINT VINCENT AND THE GRENADINES \| \|

\| 224 \|VE \|VENEZUELA \| \|

\| 225 \|VG \|VIRGIN ISLANDS \(BRITISH\) \| \|

\| 226 \|VI \|VIRGIN ISLANDS \(U.S.\) \| \|

\| 227 \|VN \|VIETNAM \| \|

\| 228 \|VU \|VANUATU \| \|

\| 229 \|WF \|WALLIS AND FUTUNA ISLANDS \| \|

\| 230 \|WS \|SAMOA \| \|

\| 231 \|YE \|YEMEN \| \|

\| 232 \|YT \|MAYOTTE \| \|

\| 233 \|YU \|YUGOSLAVIA \| \|

\| 234 \|ZA \|SOUTH AFRICA \| \|

\| 235 \|ZM \|ZAMBIA \| \|

\| 236 \|ZR \|ZAIRE \| \|

\| 237 \|ZW \|ZIMBABWE \| \| 


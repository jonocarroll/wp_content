---
ID: 202
post_title: '&pi;, visualised'
author: Jonathan Carroll
post_date: 2013-04-09 11:31:07
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2013/04/09/visualised/
published: true
---
Out of interest, I felt like visualising the digits of π. Nerd? Never.<!--more-->

I've calculated π using the usual arctan formula, to enough digits for what I'm planning; 3600. 
<code>
3.141592653589793238462643383279502884197169399375105820974944592307816406286208998628034825342117067982148086513282306647093844609550582231725359408128481117450284102701938521105559644622948954930381964428810975665933446128475648233786783165271201909145648566923460348610454326648213393607260249141273724587006606315588174881520920962829254091715364367892590360011330530548820466521384146951941511609433057270365759591953092186117381932611793105118548074462379962749567351885752724891227938183011949129833673362440656643086021394946395224737190702179860943702770539217176293176752384674818467669405132000568127145263560827785771342757789609173637178721468440901224953430146549585371050792279689258923542019956112129021960864034418159813629774771309960518707211349999998372978049951059731732816096318595024459455346908302642522308253344685035261931188171010003137838752886587533208381420617177669147303598253490428755468731159562863882353787593751957781857780532171226806613001927876611195909216420198938095257201065485863278865936153381827968230301952035301852968995773622599413891249721775283479131515574857242454150695950829533116861727855889075098381754637464939319255060400927701671139009848824012858361603563707660104710181942955596198946767837449448255379774726847104047534646208046684259069491293313677028989152104752162056966024058038150193511253382430035587640247496473263914199272604269922796782354781636009341721641219924586315030286182974555706749838505494588586926995690927210797509302955321165344987202755960236480665499119881834797753566369807426542527862551818417574672890977772793800081647060016145249192173217214772350141441973568548161361157352552133475741849468438523323907394143334547762416862518983569485562099219222184272550254256887671790494601653466804988627232791786085784383827967976681454100953883786360950680064225125205117392984896084128488626945604241965285022210661186306744278622039194945047123713786960956364371917287467764657573962413890865832645995813390478027590099465764078951269468398352595709825822620522489407726719478268482601476990902640136394437455305068203496252451749399651431429809190659250937221696461515709858387410597885959772975498930161753928468138268683868942774155991855925245953959431049972524680845987273644695848653836736222626099124608051243884390451244136549762780797715691435997700129616089441694868555848406353422072225828488648158456028506016842739452267467678895252138522549954666727823986456596116354886230577456498035593634568174324112515076069479451096596094025228879710893145669136867228748940560101503308617928680920874760917824938589009714909675985261365549781893129784821682998948722658804857564014270477555132379641451523746234364542858444795265867821051141354735739523113427166102135969536231442952484937187110145765403590279934403742007310578539062198387447808478489683321445713868751943506430218453191048481005370614680674919278191197939952061419663428754440643745123718192179998391015919561814675142691239748940907186494231961567945208095146550225231603881930142093762137855956638937787083039069792077346722182562599661501421503068038447734549202605414665925201497442850732518666002132434088190710486331734649651453905796268561005508106658796998163574736384052571459102897064140110971206280439039759515677157700420337869936007230558763176359421873125147120532928191826186125867321579198414848829164470609575270695722091756711672291098169091528017350671274858322287183520935396572512108357915136988209144421006751033467110314126711136990865851639831501970165151168517143765761835155650884909989859982387345528331635507647918532
</code>

I take the first three digits after the decimal (=141), modulo 255 (=141), and use these as the R in an RGB triple. I do the same for the next three digits (=592), modulo 255 (=82) and use these as the G value. Then the three after that (653 -&gt; 143 -&gt; B value). So the first RGB triple is (141,82,143) which looks like this <font size="+4" color="#8D528F">&#x25a0;</font>. Then I start another RGB triple and do the whole thing over and over again, until I have 400 values. Each triple is used to draw a pixel using the Imagemagick tool in a 20x20 grid png file, which I've magnified 20x. The result is:

[caption id="attachment_203" align="aligncenter" width="400"]<a href="http://jcarroll.com.au/wp-content/uploads/2013/04/draw_pi.png"><img src="http://jcarroll.com.au/wp-content/uploads/2013/04/draw_pi.png" alt="pi, visualised" width="400" height="400" class="size-full wp-image-203" /></a> pi, visualised[/caption]

<br /><br />

The source for this is below. I'm yet to figure out how to loop over arguments for Imagemagick (it didn't like me echoing to it from a subshell), so there's a lot of lines for adding the pixels.

[bash]
#!/bin/bash

export BC_LINE_LENGTH=4000

length=3600

pi=$(echo &quot;scale=$length; 4*a(1)&quot; | bc -l)
echo $pi

j=0

for i in $(seq 2 9 $length) ; do

    pisub1=${pi:$i:3}
    pisub2=${pi:$(($i+3)):3}
    pisub3=${pi:$(($i+6)):3}

    pisub1mod[j]=$(echo &quot;$pisub1 % 255&quot; | bc)
    pisub2mod[j]=$(echo &quot;$pisub2 % 255&quot; | bc)
    pisub3mod[j]=$(echo &quot;$pisub3 % 255&quot; | bc)

    j=$(($j+1))

done

convert -size 20x20 xc:white \
-fill &quot;rgb(${pisub1mod[0]},${pisub2mod[0]},${pisub3mod[0]})&quot; -draw &quot;point 0,0&quot; \
-fill &quot;rgb(${pisub1mod[1]},${pisub2mod[1]},${pisub3mod[1]})&quot; -draw &quot;point 1,0&quot; \
-fill &quot;rgb(${pisub1mod[2]},${pisub2mod[2]},${pisub3mod[2]})&quot; -draw &quot;point 2,0&quot; \
-fill &quot;rgb(${pisub1mod[3]},${pisub2mod[3]},${pisub3mod[3]})&quot; -draw &quot;point 3,0&quot; \
-fill &quot;rgb(${pisub1mod[4]},${pisub2mod[4]},${pisub3mod[4]})&quot; -draw &quot;point 4,0&quot; \
-fill &quot;rgb(${pisub1mod[5]},${pisub2mod[5]},${pisub3mod[5]})&quot; -draw &quot;point 5,0&quot; \
-fill &quot;rgb(${pisub1mod[6]},${pisub2mod[6]},${pisub3mod[6]})&quot; -draw &quot;point 6,0&quot; \
-fill &quot;rgb(${pisub1mod[7]},${pisub2mod[7]},${pisub3mod[7]})&quot; -draw &quot;point 7,0&quot; \
-fill &quot;rgb(${pisub1mod[8]},${pisub2mod[8]},${pisub3mod[8]})&quot; -draw &quot;point 8,0&quot; \
-fill &quot;rgb(${pisub1mod[9]},${pisub2mod[9]},${pisub3mod[9]})&quot; -draw &quot;point 9,0&quot; \
-fill &quot;rgb(${pisub1mod[10]},${pisub2mod[10]},${pisub3mod[10]})&quot; -draw &quot;point 10,0&quot; \
-fill &quot;rgb(${pisub1mod[11]},${pisub2mod[11]},${pisub3mod[11]})&quot; -draw &quot;point 11,0&quot; \
-fill &quot;rgb(${pisub1mod[12]},${pisub2mod[12]},${pisub3mod[12]})&quot; -draw &quot;point 12,0&quot; \
-fill &quot;rgb(${pisub1mod[13]},${pisub2mod[13]},${pisub3mod[13]})&quot; -draw &quot;point 13,0&quot; \
-fill &quot;rgb(${pisub1mod[14]},${pisub2mod[14]},${pisub3mod[14]})&quot; -draw &quot;point 14,0&quot; \
-fill &quot;rgb(${pisub1mod[15]},${pisub2mod[15]},${pisub3mod[15]})&quot; -draw &quot;point 15,0&quot; \
-fill &quot;rgb(${pisub1mod[16]},${pisub2mod[16]},${pisub3mod[16]})&quot; -draw &quot;point 16,0&quot; \
-fill &quot;rgb(${pisub1mod[17]},${pisub2mod[17]},${pisub3mod[17]})&quot; -draw &quot;point 17,0&quot; \
-fill &quot;rgb(${pisub1mod[18]},${pisub2mod[18]},${pisub3mod[18]})&quot; -draw &quot;point 18,0&quot; \
-fill &quot;rgb(${pisub1mod[19]},${pisub2mod[19]},${pisub3mod[19]})&quot; -draw &quot;point 19,0&quot; \
-fill &quot;rgb(${pisub1mod[20]},${pisub2mod[20]},${pisub3mod[20]})&quot; -draw &quot;point 0,1&quot; \
-fill &quot;rgb(${pisub1mod[21]},${pisub2mod[21]},${pisub3mod[21]})&quot; -draw &quot;point 1,1&quot; \
-fill &quot;rgb(${pisub1mod[22]},${pisub2mod[22]},${pisub3mod[22]})&quot; -draw &quot;point 2,1&quot; \
-fill &quot;rgb(${pisub1mod[23]},${pisub2mod[23]},${pisub3mod[23]})&quot; -draw &quot;point 3,1&quot; \
-fill &quot;rgb(${pisub1mod[24]},${pisub2mod[24]},${pisub3mod[24]})&quot; -draw &quot;point 4,1&quot; \
-fill &quot;rgb(${pisub1mod[25]},${pisub2mod[25]},${pisub3mod[25]})&quot; -draw &quot;point 5,1&quot; \
-fill &quot;rgb(${pisub1mod[26]},${pisub2mod[26]},${pisub3mod[26]})&quot; -draw &quot;point 6,1&quot; \
-fill &quot;rgb(${pisub1mod[27]},${pisub2mod[27]},${pisub3mod[27]})&quot; -draw &quot;point 7,1&quot; \
-fill &quot;rgb(${pisub1mod[28]},${pisub2mod[28]},${pisub3mod[28]})&quot; -draw &quot;point 8,1&quot; \
-fill &quot;rgb(${pisub1mod[29]},${pisub2mod[29]},${pisub3mod[29]})&quot; -draw &quot;point 9,1&quot; \
-fill &quot;rgb(${pisub1mod[30]},${pisub2mod[30]},${pisub3mod[30]})&quot; -draw &quot;point 10,1&quot; \
-fill &quot;rgb(${pisub1mod[31]},${pisub2mod[31]},${pisub3mod[31]})&quot; -draw &quot;point 11,1&quot; \
-fill &quot;rgb(${pisub1mod[32]},${pisub2mod[32]},${pisub3mod[32]})&quot; -draw &quot;point 12,1&quot; \
-fill &quot;rgb(${pisub1mod[33]},${pisub2mod[33]},${pisub3mod[33]})&quot; -draw &quot;point 13,1&quot; \
-fill &quot;rgb(${pisub1mod[34]},${pisub2mod[34]},${pisub3mod[34]})&quot; -draw &quot;point 14,1&quot; \
-fill &quot;rgb(${pisub1mod[35]},${pisub2mod[35]},${pisub3mod[35]})&quot; -draw &quot;point 15,1&quot; \
-fill &quot;rgb(${pisub1mod[36]},${pisub2mod[36]},${pisub3mod[36]})&quot; -draw &quot;point 16,1&quot; \
-fill &quot;rgb(${pisub1mod[37]},${pisub2mod[37]},${pisub3mod[37]})&quot; -draw &quot;point 17,1&quot; \
-fill &quot;rgb(${pisub1mod[38]},${pisub2mod[38]},${pisub3mod[38]})&quot; -draw &quot;point 18,1&quot; \
-fill &quot;rgb(${pisub1mod[39]},${pisub2mod[39]},${pisub3mod[39]})&quot; -draw &quot;point 19,1&quot; \
-fill &quot;rgb(${pisub1mod[40]},${pisub2mod[40]},${pisub3mod[40]})&quot; -draw &quot;point 0,2&quot; \
-fill &quot;rgb(${pisub1mod[41]},${pisub2mod[41]},${pisub3mod[41]})&quot; -draw &quot;point 1,2&quot; \
-fill &quot;rgb(${pisub1mod[42]},${pisub2mod[42]},${pisub3mod[42]})&quot; -draw &quot;point 2,2&quot; \
-fill &quot;rgb(${pisub1mod[43]},${pisub2mod[43]},${pisub3mod[43]})&quot; -draw &quot;point 3,2&quot; \
-fill &quot;rgb(${pisub1mod[44]},${pisub2mod[44]},${pisub3mod[44]})&quot; -draw &quot;point 4,2&quot; \
-fill &quot;rgb(${pisub1mod[45]},${pisub2mod[45]},${pisub3mod[45]})&quot; -draw &quot;point 5,2&quot; \
-fill &quot;rgb(${pisub1mod[46]},${pisub2mod[46]},${pisub3mod[46]})&quot; -draw &quot;point 6,2&quot; \
-fill &quot;rgb(${pisub1mod[47]},${pisub2mod[47]},${pisub3mod[47]})&quot; -draw &quot;point 7,2&quot; \
-fill &quot;rgb(${pisub1mod[48]},${pisub2mod[48]},${pisub3mod[48]})&quot; -draw &quot;point 8,2&quot; \
-fill &quot;rgb(${pisub1mod[49]},${pisub2mod[49]},${pisub3mod[49]})&quot; -draw &quot;point 9,2&quot; \
-fill &quot;rgb(${pisub1mod[50]},${pisub2mod[50]},${pisub3mod[50]})&quot; -draw &quot;point 10,2&quot; \
-fill &quot;rgb(${pisub1mod[51]},${pisub2mod[51]},${pisub3mod[51]})&quot; -draw &quot;point 11,2&quot; \
-fill &quot;rgb(${pisub1mod[52]},${pisub2mod[52]},${pisub3mod[52]})&quot; -draw &quot;point 12,2&quot; \
-fill &quot;rgb(${pisub1mod[53]},${pisub2mod[53]},${pisub3mod[53]})&quot; -draw &quot;point 13,2&quot; \
-fill &quot;rgb(${pisub1mod[54]},${pisub2mod[54]},${pisub3mod[54]})&quot; -draw &quot;point 14,2&quot; \
-fill &quot;rgb(${pisub1mod[55]},${pisub2mod[55]},${pisub3mod[55]})&quot; -draw &quot;point 15,2&quot; \
-fill &quot;rgb(${pisub1mod[56]},${pisub2mod[56]},${pisub3mod[56]})&quot; -draw &quot;point 16,2&quot; \
-fill &quot;rgb(${pisub1mod[57]},${pisub2mod[57]},${pisub3mod[57]})&quot; -draw &quot;point 17,2&quot; \
-fill &quot;rgb(${pisub1mod[58]},${pisub2mod[58]},${pisub3mod[58]})&quot; -draw &quot;point 18,2&quot; \
-fill &quot;rgb(${pisub1mod[59]},${pisub2mod[59]},${pisub3mod[59]})&quot; -draw &quot;point 19,2&quot; \
-fill &quot;rgb(${pisub1mod[60]},${pisub2mod[60]},${pisub3mod[60]})&quot; -draw &quot;point 0,3&quot; \
-fill &quot;rgb(${pisub1mod[61]},${pisub2mod[61]},${pisub3mod[61]})&quot; -draw &quot;point 1,3&quot; \
-fill &quot;rgb(${pisub1mod[62]},${pisub2mod[62]},${pisub3mod[62]})&quot; -draw &quot;point 2,3&quot; \
-fill &quot;rgb(${pisub1mod[63]},${pisub2mod[63]},${pisub3mod[63]})&quot; -draw &quot;point 3,3&quot; \
-fill &quot;rgb(${pisub1mod[64]},${pisub2mod[64]},${pisub3mod[64]})&quot; -draw &quot;point 4,3&quot; \
-fill &quot;rgb(${pisub1mod[65]},${pisub2mod[65]},${pisub3mod[65]})&quot; -draw &quot;point 5,3&quot; \
-fill &quot;rgb(${pisub1mod[66]},${pisub2mod[66]},${pisub3mod[66]})&quot; -draw &quot;point 6,3&quot; \
-fill &quot;rgb(${pisub1mod[67]},${pisub2mod[67]},${pisub3mod[67]})&quot; -draw &quot;point 7,3&quot; \
-fill &quot;rgb(${pisub1mod[68]},${pisub2mod[68]},${pisub3mod[68]})&quot; -draw &quot;point 8,3&quot; \
-fill &quot;rgb(${pisub1mod[69]},${pisub2mod[69]},${pisub3mod[69]})&quot; -draw &quot;point 9,3&quot; \
-fill &quot;rgb(${pisub1mod[70]},${pisub2mod[70]},${pisub3mod[70]})&quot; -draw &quot;point 10,3&quot; \
-fill &quot;rgb(${pisub1mod[71]},${pisub2mod[71]},${pisub3mod[71]})&quot; -draw &quot;point 11,3&quot; \
-fill &quot;rgb(${pisub1mod[72]},${pisub2mod[72]},${pisub3mod[72]})&quot; -draw &quot;point 12,3&quot; \
-fill &quot;rgb(${pisub1mod[73]},${pisub2mod[73]},${pisub3mod[73]})&quot; -draw &quot;point 13,3&quot; \
-fill &quot;rgb(${pisub1mod[74]},${pisub2mod[74]},${pisub3mod[74]})&quot; -draw &quot;point 14,3&quot; \
-fill &quot;rgb(${pisub1mod[75]},${pisub2mod[75]},${pisub3mod[75]})&quot; -draw &quot;point 15,3&quot; \
-fill &quot;rgb(${pisub1mod[76]},${pisub2mod[76]},${pisub3mod[76]})&quot; -draw &quot;point 16,3&quot; \
-fill &quot;rgb(${pisub1mod[77]},${pisub2mod[77]},${pisub3mod[77]})&quot; -draw &quot;point 17,3&quot; \
-fill &quot;rgb(${pisub1mod[78]},${pisub2mod[78]},${pisub3mod[78]})&quot; -draw &quot;point 18,3&quot; \
-fill &quot;rgb(${pisub1mod[79]},${pisub2mod[79]},${pisub3mod[79]})&quot; -draw &quot;point 19,3&quot; \
-fill &quot;rgb(${pisub1mod[80]},${pisub2mod[80]},${pisub3mod[80]})&quot; -draw &quot;point 0,4&quot; \
-fill &quot;rgb(${pisub1mod[81]},${pisub2mod[81]},${pisub3mod[81]})&quot; -draw &quot;point 1,4&quot; \
-fill &quot;rgb(${pisub1mod[82]},${pisub2mod[82]},${pisub3mod[82]})&quot; -draw &quot;point 2,4&quot; \
-fill &quot;rgb(${pisub1mod[83]},${pisub2mod[83]},${pisub3mod[83]})&quot; -draw &quot;point 3,4&quot; \
-fill &quot;rgb(${pisub1mod[84]},${pisub2mod[84]},${pisub3mod[84]})&quot; -draw &quot;point 4,4&quot; \
-fill &quot;rgb(${pisub1mod[85]},${pisub2mod[85]},${pisub3mod[85]})&quot; -draw &quot;point 5,4&quot; \
-fill &quot;rgb(${pisub1mod[86]},${pisub2mod[86]},${pisub3mod[86]})&quot; -draw &quot;point 6,4&quot; \
-fill &quot;rgb(${pisub1mod[87]},${pisub2mod[87]},${pisub3mod[87]})&quot; -draw &quot;point 7,4&quot; \
-fill &quot;rgb(${pisub1mod[88]},${pisub2mod[88]},${pisub3mod[88]})&quot; -draw &quot;point 8,4&quot; \
-fill &quot;rgb(${pisub1mod[89]},${pisub2mod[89]},${pisub3mod[89]})&quot; -draw &quot;point 9,4&quot; \
-fill &quot;rgb(${pisub1mod[90]},${pisub2mod[90]},${pisub3mod[90]})&quot; -draw &quot;point 10,4&quot; \
-fill &quot;rgb(${pisub1mod[91]},${pisub2mod[91]},${pisub3mod[91]})&quot; -draw &quot;point 11,4&quot; \
-fill &quot;rgb(${pisub1mod[92]},${pisub2mod[92]},${pisub3mod[92]})&quot; -draw &quot;point 12,4&quot; \
-fill &quot;rgb(${pisub1mod[93]},${pisub2mod[93]},${pisub3mod[93]})&quot; -draw &quot;point 13,4&quot; \
-fill &quot;rgb(${pisub1mod[94]},${pisub2mod[94]},${pisub3mod[94]})&quot; -draw &quot;point 14,4&quot; \
-fill &quot;rgb(${pisub1mod[95]},${pisub2mod[95]},${pisub3mod[95]})&quot; -draw &quot;point 15,4&quot; \
-fill &quot;rgb(${pisub1mod[96]},${pisub2mod[96]},${pisub3mod[96]})&quot; -draw &quot;point 16,4&quot; \
-fill &quot;rgb(${pisub1mod[97]},${pisub2mod[97]},${pisub3mod[97]})&quot; -draw &quot;point 17,4&quot; \
-fill &quot;rgb(${pisub1mod[98]},${pisub2mod[98]},${pisub3mod[98]})&quot; -draw &quot;point 18,4&quot; \
-fill &quot;rgb(${pisub1mod[99]},${pisub2mod[99]},${pisub3mod[99]})&quot; -draw &quot;point 19,4&quot; \
-fill &quot;rgb(${pisub1mod[100]},${pisub2mod[100]},${pisub3mod[100]})&quot; -draw &quot;point 0,5&quot; \
-fill &quot;rgb(${pisub1mod[101]},${pisub2mod[101]},${pisub3mod[101]})&quot; -draw &quot;point 1,5&quot; \
-fill &quot;rgb(${pisub1mod[102]},${pisub2mod[102]},${pisub3mod[102]})&quot; -draw &quot;point 2,5&quot; \
-fill &quot;rgb(${pisub1mod[103]},${pisub2mod[103]},${pisub3mod[103]})&quot; -draw &quot;point 3,5&quot; \
-fill &quot;rgb(${pisub1mod[104]},${pisub2mod[104]},${pisub3mod[104]})&quot; -draw &quot;point 4,5&quot; \
-fill &quot;rgb(${pisub1mod[105]},${pisub2mod[105]},${pisub3mod[105]})&quot; -draw &quot;point 5,5&quot; \
-fill &quot;rgb(${pisub1mod[106]},${pisub2mod[106]},${pisub3mod[106]})&quot; -draw &quot;point 6,5&quot; \
-fill &quot;rgb(${pisub1mod[107]},${pisub2mod[107]},${pisub3mod[107]})&quot; -draw &quot;point 7,5&quot; \
-fill &quot;rgb(${pisub1mod[108]},${pisub2mod[108]},${pisub3mod[108]})&quot; -draw &quot;point 8,5&quot; \
-fill &quot;rgb(${pisub1mod[109]},${pisub2mod[109]},${pisub3mod[109]})&quot; -draw &quot;point 9,5&quot; \
-fill &quot;rgb(${pisub1mod[110]},${pisub2mod[110]},${pisub3mod[110]})&quot; -draw &quot;point 10,5&quot; \
-fill &quot;rgb(${pisub1mod[111]},${pisub2mod[111]},${pisub3mod[111]})&quot; -draw &quot;point 11,5&quot; \
-fill &quot;rgb(${pisub1mod[112]},${pisub2mod[112]},${pisub3mod[112]})&quot; -draw &quot;point 12,5&quot; \
-fill &quot;rgb(${pisub1mod[113]},${pisub2mod[113]},${pisub3mod[113]})&quot; -draw &quot;point 13,5&quot; \
-fill &quot;rgb(${pisub1mod[114]},${pisub2mod[114]},${pisub3mod[114]})&quot; -draw &quot;point 14,5&quot; \
-fill &quot;rgb(${pisub1mod[115]},${pisub2mod[115]},${pisub3mod[115]})&quot; -draw &quot;point 15,5&quot; \
-fill &quot;rgb(${pisub1mod[116]},${pisub2mod[116]},${pisub3mod[116]})&quot; -draw &quot;point 16,5&quot; \
-fill &quot;rgb(${pisub1mod[117]},${pisub2mod[117]},${pisub3mod[117]})&quot; -draw &quot;point 17,5&quot; \
-fill &quot;rgb(${pisub1mod[118]},${pisub2mod[118]},${pisub3mod[118]})&quot; -draw &quot;point 18,5&quot; \
-fill &quot;rgb(${pisub1mod[119]},${pisub2mod[119]},${pisub3mod[119]})&quot; -draw &quot;point 19,5&quot; \
-fill &quot;rgb(${pisub1mod[120]},${pisub2mod[120]},${pisub3mod[120]})&quot; -draw &quot;point 0,6&quot; \
-fill &quot;rgb(${pisub1mod[121]},${pisub2mod[121]},${pisub3mod[121]})&quot; -draw &quot;point 1,6&quot; \
-fill &quot;rgb(${pisub1mod[122]},${pisub2mod[122]},${pisub3mod[122]})&quot; -draw &quot;point 2,6&quot; \
-fill &quot;rgb(${pisub1mod[123]},${pisub2mod[123]},${pisub3mod[123]})&quot; -draw &quot;point 3,6&quot; \
-fill &quot;rgb(${pisub1mod[124]},${pisub2mod[124]},${pisub3mod[124]})&quot; -draw &quot;point 4,6&quot; \
-fill &quot;rgb(${pisub1mod[125]},${pisub2mod[125]},${pisub3mod[125]})&quot; -draw &quot;point 5,6&quot; \
-fill &quot;rgb(${pisub1mod[126]},${pisub2mod[126]},${pisub3mod[126]})&quot; -draw &quot;point 6,6&quot; \
-fill &quot;rgb(${pisub1mod[127]},${pisub2mod[127]},${pisub3mod[127]})&quot; -draw &quot;point 7,6&quot; \
-fill &quot;rgb(${pisub1mod[128]},${pisub2mod[128]},${pisub3mod[128]})&quot; -draw &quot;point 8,6&quot; \
-fill &quot;rgb(${pisub1mod[129]},${pisub2mod[129]},${pisub3mod[129]})&quot; -draw &quot;point 9,6&quot; \
-fill &quot;rgb(${pisub1mod[130]},${pisub2mod[130]},${pisub3mod[130]})&quot; -draw &quot;point 10,6&quot; \
-fill &quot;rgb(${pisub1mod[131]},${pisub2mod[131]},${pisub3mod[131]})&quot; -draw &quot;point 11,6&quot; \
-fill &quot;rgb(${pisub1mod[132]},${pisub2mod[132]},${pisub3mod[132]})&quot; -draw &quot;point 12,6&quot; \
-fill &quot;rgb(${pisub1mod[133]},${pisub2mod[133]},${pisub3mod[133]})&quot; -draw &quot;point 13,6&quot; \
-fill &quot;rgb(${pisub1mod[134]},${pisub2mod[134]},${pisub3mod[134]})&quot; -draw &quot;point 14,6&quot; \
-fill &quot;rgb(${pisub1mod[135]},${pisub2mod[135]},${pisub3mod[135]})&quot; -draw &quot;point 15,6&quot; \
-fill &quot;rgb(${pisub1mod[136]},${pisub2mod[136]},${pisub3mod[136]})&quot; -draw &quot;point 16,6&quot; \
-fill &quot;rgb(${pisub1mod[137]},${pisub2mod[137]},${pisub3mod[137]})&quot; -draw &quot;point 17,6&quot; \
-fill &quot;rgb(${pisub1mod[138]},${pisub2mod[138]},${pisub3mod[138]})&quot; -draw &quot;point 18,6&quot; \
-fill &quot;rgb(${pisub1mod[139]},${pisub2mod[139]},${pisub3mod[139]})&quot; -draw &quot;point 19,6&quot; \
-fill &quot;rgb(${pisub1mod[140]},${pisub2mod[140]},${pisub3mod[140]})&quot; -draw &quot;point 0,7&quot; \
-fill &quot;rgb(${pisub1mod[141]},${pisub2mod[141]},${pisub3mod[141]})&quot; -draw &quot;point 1,7&quot; \
-fill &quot;rgb(${pisub1mod[142]},${pisub2mod[142]},${pisub3mod[142]})&quot; -draw &quot;point 2,7&quot; \
-fill &quot;rgb(${pisub1mod[143]},${pisub2mod[143]},${pisub3mod[143]})&quot; -draw &quot;point 3,7&quot; \
-fill &quot;rgb(${pisub1mod[144]},${pisub2mod[144]},${pisub3mod[144]})&quot; -draw &quot;point 4,7&quot; \
-fill &quot;rgb(${pisub1mod[145]},${pisub2mod[145]},${pisub3mod[145]})&quot; -draw &quot;point 5,7&quot; \
-fill &quot;rgb(${pisub1mod[146]},${pisub2mod[146]},${pisub3mod[146]})&quot; -draw &quot;point 6,7&quot; \
-fill &quot;rgb(${pisub1mod[147]},${pisub2mod[147]},${pisub3mod[147]})&quot; -draw &quot;point 7,7&quot; \
-fill &quot;rgb(${pisub1mod[148]},${pisub2mod[148]},${pisub3mod[148]})&quot; -draw &quot;point 8,7&quot; \
-fill &quot;rgb(${pisub1mod[149]},${pisub2mod[149]},${pisub3mod[149]})&quot; -draw &quot;point 9,7&quot; \
-fill &quot;rgb(${pisub1mod[150]},${pisub2mod[150]},${pisub3mod[150]})&quot; -draw &quot;point 10,7&quot; \
-fill &quot;rgb(${pisub1mod[151]},${pisub2mod[151]},${pisub3mod[151]})&quot; -draw &quot;point 11,7&quot; \
-fill &quot;rgb(${pisub1mod[152]},${pisub2mod[152]},${pisub3mod[152]})&quot; -draw &quot;point 12,7&quot; \
-fill &quot;rgb(${pisub1mod[153]},${pisub2mod[153]},${pisub3mod[153]})&quot; -draw &quot;point 13,7&quot; \
-fill &quot;rgb(${pisub1mod[154]},${pisub2mod[154]},${pisub3mod[154]})&quot; -draw &quot;point 14,7&quot; \
-fill &quot;rgb(${pisub1mod[155]},${pisub2mod[155]},${pisub3mod[155]})&quot; -draw &quot;point 15,7&quot; \
-fill &quot;rgb(${pisub1mod[156]},${pisub2mod[156]},${pisub3mod[156]})&quot; -draw &quot;point 16,7&quot; \
-fill &quot;rgb(${pisub1mod[157]},${pisub2mod[157]},${pisub3mod[157]})&quot; -draw &quot;point 17,7&quot; \
-fill &quot;rgb(${pisub1mod[158]},${pisub2mod[158]},${pisub3mod[158]})&quot; -draw &quot;point 18,7&quot; \
-fill &quot;rgb(${pisub1mod[159]},${pisub2mod[159]},${pisub3mod[159]})&quot; -draw &quot;point 19,7&quot; \
-fill &quot;rgb(${pisub1mod[160]},${pisub2mod[160]},${pisub3mod[160]})&quot; -draw &quot;point 0,8&quot; \
-fill &quot;rgb(${pisub1mod[161]},${pisub2mod[161]},${pisub3mod[161]})&quot; -draw &quot;point 1,8&quot; \
-fill &quot;rgb(${pisub1mod[162]},${pisub2mod[162]},${pisub3mod[162]})&quot; -draw &quot;point 2,8&quot; \
-fill &quot;rgb(${pisub1mod[163]},${pisub2mod[163]},${pisub3mod[163]})&quot; -draw &quot;point 3,8&quot; \
-fill &quot;rgb(${pisub1mod[164]},${pisub2mod[164]},${pisub3mod[164]})&quot; -draw &quot;point 4,8&quot; \
-fill &quot;rgb(${pisub1mod[165]},${pisub2mod[165]},${pisub3mod[165]})&quot; -draw &quot;point 5,8&quot; \
-fill &quot;rgb(${pisub1mod[166]},${pisub2mod[166]},${pisub3mod[166]})&quot; -draw &quot;point 6,8&quot; \
-fill &quot;rgb(${pisub1mod[167]},${pisub2mod[167]},${pisub3mod[167]})&quot; -draw &quot;point 7,8&quot; \
-fill &quot;rgb(${pisub1mod[168]},${pisub2mod[168]},${pisub3mod[168]})&quot; -draw &quot;point 8,8&quot; \
-fill &quot;rgb(${pisub1mod[169]},${pisub2mod[169]},${pisub3mod[169]})&quot; -draw &quot;point 9,8&quot; \
-fill &quot;rgb(${pisub1mod[170]},${pisub2mod[170]},${pisub3mod[170]})&quot; -draw &quot;point 10,8&quot; \
-fill &quot;rgb(${pisub1mod[171]},${pisub2mod[171]},${pisub3mod[171]})&quot; -draw &quot;point 11,8&quot; \
-fill &quot;rgb(${pisub1mod[172]},${pisub2mod[172]},${pisub3mod[172]})&quot; -draw &quot;point 12,8&quot; \
-fill &quot;rgb(${pisub1mod[173]},${pisub2mod[173]},${pisub3mod[173]})&quot; -draw &quot;point 13,8&quot; \
-fill &quot;rgb(${pisub1mod[174]},${pisub2mod[174]},${pisub3mod[174]})&quot; -draw &quot;point 14,8&quot; \
-fill &quot;rgb(${pisub1mod[175]},${pisub2mod[175]},${pisub3mod[175]})&quot; -draw &quot;point 15,8&quot; \
-fill &quot;rgb(${pisub1mod[176]},${pisub2mod[176]},${pisub3mod[176]})&quot; -draw &quot;point 16,8&quot; \
-fill &quot;rgb(${pisub1mod[177]},${pisub2mod[177]},${pisub3mod[177]})&quot; -draw &quot;point 17,8&quot; \
-fill &quot;rgb(${pisub1mod[178]},${pisub2mod[178]},${pisub3mod[178]})&quot; -draw &quot;point 18,8&quot; \
-fill &quot;rgb(${pisub1mod[179]},${pisub2mod[179]},${pisub3mod[179]})&quot; -draw &quot;point 19,8&quot; \
-fill &quot;rgb(${pisub1mod[180]},${pisub2mod[180]},${pisub3mod[180]})&quot; -draw &quot;point 0,9&quot; \
-fill &quot;rgb(${pisub1mod[181]},${pisub2mod[181]},${pisub3mod[181]})&quot; -draw &quot;point 1,9&quot; \
-fill &quot;rgb(${pisub1mod[182]},${pisub2mod[182]},${pisub3mod[182]})&quot; -draw &quot;point 2,9&quot; \
-fill &quot;rgb(${pisub1mod[183]},${pisub2mod[183]},${pisub3mod[183]})&quot; -draw &quot;point 3,9&quot; \
-fill &quot;rgb(${pisub1mod[184]},${pisub2mod[184]},${pisub3mod[184]})&quot; -draw &quot;point 4,9&quot; \
-fill &quot;rgb(${pisub1mod[185]},${pisub2mod[185]},${pisub3mod[185]})&quot; -draw &quot;point 5,9&quot; \
-fill &quot;rgb(${pisub1mod[186]},${pisub2mod[186]},${pisub3mod[186]})&quot; -draw &quot;point 6,9&quot; \
-fill &quot;rgb(${pisub1mod[187]},${pisub2mod[187]},${pisub3mod[187]})&quot; -draw &quot;point 7,9&quot; \
-fill &quot;rgb(${pisub1mod[188]},${pisub2mod[188]},${pisub3mod[188]})&quot; -draw &quot;point 8,9&quot; \
-fill &quot;rgb(${pisub1mod[189]},${pisub2mod[189]},${pisub3mod[189]})&quot; -draw &quot;point 9,9&quot; \
-fill &quot;rgb(${pisub1mod[190]},${pisub2mod[190]},${pisub3mod[190]})&quot; -draw &quot;point 10,9&quot; \
-fill &quot;rgb(${pisub1mod[191]},${pisub2mod[191]},${pisub3mod[191]})&quot; -draw &quot;point 11,9&quot; \
-fill &quot;rgb(${pisub1mod[192]},${pisub2mod[192]},${pisub3mod[192]})&quot; -draw &quot;point 12,9&quot; \
-fill &quot;rgb(${pisub1mod[193]},${pisub2mod[193]},${pisub3mod[193]})&quot; -draw &quot;point 13,9&quot; \
-fill &quot;rgb(${pisub1mod[194]},${pisub2mod[194]},${pisub3mod[194]})&quot; -draw &quot;point 14,9&quot; \
-fill &quot;rgb(${pisub1mod[195]},${pisub2mod[195]},${pisub3mod[195]})&quot; -draw &quot;point 15,9&quot; \
-fill &quot;rgb(${pisub1mod[196]},${pisub2mod[196]},${pisub3mod[196]})&quot; -draw &quot;point 16,9&quot; \
-fill &quot;rgb(${pisub1mod[197]},${pisub2mod[197]},${pisub3mod[197]})&quot; -draw &quot;point 17,9&quot; \
-fill &quot;rgb(${pisub1mod[198]},${pisub2mod[198]},${pisub3mod[198]})&quot; -draw &quot;point 18,9&quot; \
-fill &quot;rgb(${pisub1mod[199]},${pisub2mod[199]},${pisub3mod[199]})&quot; -draw &quot;point 19,9&quot; \
-fill &quot;rgb(${pisub1mod[200]},${pisub2mod[200]},${pisub3mod[200]})&quot; -draw &quot;point 0,10&quot; \
-fill &quot;rgb(${pisub1mod[201]},${pisub2mod[201]},${pisub3mod[201]})&quot; -draw &quot;point 1,10&quot; \
-fill &quot;rgb(${pisub1mod[202]},${pisub2mod[202]},${pisub3mod[202]})&quot; -draw &quot;point 2,10&quot; \
-fill &quot;rgb(${pisub1mod[203]},${pisub2mod[203]},${pisub3mod[203]})&quot; -draw &quot;point 3,10&quot; \
-fill &quot;rgb(${pisub1mod[204]},${pisub2mod[204]},${pisub3mod[204]})&quot; -draw &quot;point 4,10&quot; \
-fill &quot;rgb(${pisub1mod[205]},${pisub2mod[205]},${pisub3mod[205]})&quot; -draw &quot;point 5,10&quot; \
-fill &quot;rgb(${pisub1mod[206]},${pisub2mod[206]},${pisub3mod[206]})&quot; -draw &quot;point 6,10&quot; \
-fill &quot;rgb(${pisub1mod[207]},${pisub2mod[207]},${pisub3mod[207]})&quot; -draw &quot;point 7,10&quot; \
-fill &quot;rgb(${pisub1mod[208]},${pisub2mod[208]},${pisub3mod[208]})&quot; -draw &quot;point 8,10&quot; \
-fill &quot;rgb(${pisub1mod[209]},${pisub2mod[209]},${pisub3mod[209]})&quot; -draw &quot;point 9,10&quot; \
-fill &quot;rgb(${pisub1mod[210]},${pisub2mod[210]},${pisub3mod[210]})&quot; -draw &quot;point 10,10&quot; \
-fill &quot;rgb(${pisub1mod[211]},${pisub2mod[211]},${pisub3mod[211]})&quot; -draw &quot;point 11,10&quot; \
-fill &quot;rgb(${pisub1mod[212]},${pisub2mod[212]},${pisub3mod[212]})&quot; -draw &quot;point 12,10&quot; \
-fill &quot;rgb(${pisub1mod[213]},${pisub2mod[213]},${pisub3mod[213]})&quot; -draw &quot;point 13,10&quot; \
-fill &quot;rgb(${pisub1mod[214]},${pisub2mod[214]},${pisub3mod[214]})&quot; -draw &quot;point 14,10&quot; \
-fill &quot;rgb(${pisub1mod[215]},${pisub2mod[215]},${pisub3mod[215]})&quot; -draw &quot;point 15,10&quot; \
-fill &quot;rgb(${pisub1mod[216]},${pisub2mod[216]},${pisub3mod[216]})&quot; -draw &quot;point 16,10&quot; \
-fill &quot;rgb(${pisub1mod[217]},${pisub2mod[217]},${pisub3mod[217]})&quot; -draw &quot;point 17,10&quot; \
-fill &quot;rgb(${pisub1mod[218]},${pisub2mod[218]},${pisub3mod[218]})&quot; -draw &quot;point 18,10&quot; \
-fill &quot;rgb(${pisub1mod[219]},${pisub2mod[219]},${pisub3mod[219]})&quot; -draw &quot;point 19,10&quot; \
-fill &quot;rgb(${pisub1mod[220]},${pisub2mod[220]},${pisub3mod[220]})&quot; -draw &quot;point 0,11&quot; \
-fill &quot;rgb(${pisub1mod[221]},${pisub2mod[221]},${pisub3mod[221]})&quot; -draw &quot;point 1,11&quot; \
-fill &quot;rgb(${pisub1mod[222]},${pisub2mod[222]},${pisub3mod[222]})&quot; -draw &quot;point 2,11&quot; \
-fill &quot;rgb(${pisub1mod[223]},${pisub2mod[223]},${pisub3mod[223]})&quot; -draw &quot;point 3,11&quot; \
-fill &quot;rgb(${pisub1mod[224]},${pisub2mod[224]},${pisub3mod[224]})&quot; -draw &quot;point 4,11&quot; \
-fill &quot;rgb(${pisub1mod[225]},${pisub2mod[225]},${pisub3mod[225]})&quot; -draw &quot;point 5,11&quot; \
-fill &quot;rgb(${pisub1mod[226]},${pisub2mod[226]},${pisub3mod[226]})&quot; -draw &quot;point 6,11&quot; \
-fill &quot;rgb(${pisub1mod[227]},${pisub2mod[227]},${pisub3mod[227]})&quot; -draw &quot;point 7,11&quot; \
-fill &quot;rgb(${pisub1mod[228]},${pisub2mod[228]},${pisub3mod[228]})&quot; -draw &quot;point 8,11&quot; \
-fill &quot;rgb(${pisub1mod[229]},${pisub2mod[229]},${pisub3mod[229]})&quot; -draw &quot;point 9,11&quot; \
-fill &quot;rgb(${pisub1mod[230]},${pisub2mod[230]},${pisub3mod[230]})&quot; -draw &quot;point 10,11&quot; \
-fill &quot;rgb(${pisub1mod[231]},${pisub2mod[231]},${pisub3mod[231]})&quot; -draw &quot;point 11,11&quot; \
-fill &quot;rgb(${pisub1mod[232]},${pisub2mod[232]},${pisub3mod[232]})&quot; -draw &quot;point 12,11&quot; \
-fill &quot;rgb(${pisub1mod[233]},${pisub2mod[233]},${pisub3mod[233]})&quot; -draw &quot;point 13,11&quot; \
-fill &quot;rgb(${pisub1mod[234]},${pisub2mod[234]},${pisub3mod[234]})&quot; -draw &quot;point 14,11&quot; \
-fill &quot;rgb(${pisub1mod[235]},${pisub2mod[235]},${pisub3mod[235]})&quot; -draw &quot;point 15,11&quot; \
-fill &quot;rgb(${pisub1mod[236]},${pisub2mod[236]},${pisub3mod[236]})&quot; -draw &quot;point 16,11&quot; \
-fill &quot;rgb(${pisub1mod[237]},${pisub2mod[237]},${pisub3mod[237]})&quot; -draw &quot;point 17,11&quot; \
-fill &quot;rgb(${pisub1mod[238]},${pisub2mod[238]},${pisub3mod[238]})&quot; -draw &quot;point 18,11&quot; \
-fill &quot;rgb(${pisub1mod[239]},${pisub2mod[239]},${pisub3mod[239]})&quot; -draw &quot;point 19,11&quot; \
-fill &quot;rgb(${pisub1mod[240]},${pisub2mod[240]},${pisub3mod[240]})&quot; -draw &quot;point 0,12&quot; \
-fill &quot;rgb(${pisub1mod[241]},${pisub2mod[241]},${pisub3mod[241]})&quot; -draw &quot;point 1,12&quot; \
-fill &quot;rgb(${pisub1mod[242]},${pisub2mod[242]},${pisub3mod[242]})&quot; -draw &quot;point 2,12&quot; \
-fill &quot;rgb(${pisub1mod[243]},${pisub2mod[243]},${pisub3mod[243]})&quot; -draw &quot;point 3,12&quot; \
-fill &quot;rgb(${pisub1mod[244]},${pisub2mod[244]},${pisub3mod[244]})&quot; -draw &quot;point 4,12&quot; \
-fill &quot;rgb(${pisub1mod[245]},${pisub2mod[245]},${pisub3mod[245]})&quot; -draw &quot;point 5,12&quot; \
-fill &quot;rgb(${pisub1mod[246]},${pisub2mod[246]},${pisub3mod[246]})&quot; -draw &quot;point 6,12&quot; \
-fill &quot;rgb(${pisub1mod[247]},${pisub2mod[247]},${pisub3mod[247]})&quot; -draw &quot;point 7,12&quot; \
-fill &quot;rgb(${pisub1mod[248]},${pisub2mod[248]},${pisub3mod[248]})&quot; -draw &quot;point 8,12&quot; \
-fill &quot;rgb(${pisub1mod[249]},${pisub2mod[249]},${pisub3mod[249]})&quot; -draw &quot;point 9,12&quot; \
-fill &quot;rgb(${pisub1mod[250]},${pisub2mod[250]},${pisub3mod[250]})&quot; -draw &quot;point 10,12&quot; \
-fill &quot;rgb(${pisub1mod[251]},${pisub2mod[251]},${pisub3mod[251]})&quot; -draw &quot;point 11,12&quot; \
-fill &quot;rgb(${pisub1mod[252]},${pisub2mod[252]},${pisub3mod[252]})&quot; -draw &quot;point 12,12&quot; \
-fill &quot;rgb(${pisub1mod[253]},${pisub2mod[253]},${pisub3mod[253]})&quot; -draw &quot;point 13,12&quot; \
-fill &quot;rgb(${pisub1mod[254]},${pisub2mod[254]},${pisub3mod[254]})&quot; -draw &quot;point 14,12&quot; \
-fill &quot;rgb(${pisub1mod[255]},${pisub2mod[255]},${pisub3mod[255]})&quot; -draw &quot;point 15,12&quot; \
-fill &quot;rgb(${pisub1mod[256]},${pisub2mod[256]},${pisub3mod[256]})&quot; -draw &quot;point 16,12&quot; \
-fill &quot;rgb(${pisub1mod[257]},${pisub2mod[257]},${pisub3mod[257]})&quot; -draw &quot;point 17,12&quot; \
-fill &quot;rgb(${pisub1mod[258]},${pisub2mod[258]},${pisub3mod[258]})&quot; -draw &quot;point 18,12&quot; \
-fill &quot;rgb(${pisub1mod[259]},${pisub2mod[259]},${pisub3mod[259]})&quot; -draw &quot;point 19,12&quot; \
-fill &quot;rgb(${pisub1mod[260]},${pisub2mod[260]},${pisub3mod[260]})&quot; -draw &quot;point 0,13&quot; \
-fill &quot;rgb(${pisub1mod[261]},${pisub2mod[261]},${pisub3mod[261]})&quot; -draw &quot;point 1,13&quot; \
-fill &quot;rgb(${pisub1mod[262]},${pisub2mod[262]},${pisub3mod[262]})&quot; -draw &quot;point 2,13&quot; \
-fill &quot;rgb(${pisub1mod[263]},${pisub2mod[263]},${pisub3mod[263]})&quot; -draw &quot;point 3,13&quot; \
-fill &quot;rgb(${pisub1mod[264]},${pisub2mod[264]},${pisub3mod[264]})&quot; -draw &quot;point 4,13&quot; \
-fill &quot;rgb(${pisub1mod[265]},${pisub2mod[265]},${pisub3mod[265]})&quot; -draw &quot;point 5,13&quot; \
-fill &quot;rgb(${pisub1mod[266]},${pisub2mod[266]},${pisub3mod[266]})&quot; -draw &quot;point 6,13&quot; \
-fill &quot;rgb(${pisub1mod[267]},${pisub2mod[267]},${pisub3mod[267]})&quot; -draw &quot;point 7,13&quot; \
-fill &quot;rgb(${pisub1mod[268]},${pisub2mod[268]},${pisub3mod[268]})&quot; -draw &quot;point 8,13&quot; \
-fill &quot;rgb(${pisub1mod[269]},${pisub2mod[269]},${pisub3mod[269]})&quot; -draw &quot;point 9,13&quot; \
-fill &quot;rgb(${pisub1mod[270]},${pisub2mod[270]},${pisub3mod[270]})&quot; -draw &quot;point 10,13&quot; \
-fill &quot;rgb(${pisub1mod[271]},${pisub2mod[271]},${pisub3mod[271]})&quot; -draw &quot;point 11,13&quot; \
-fill &quot;rgb(${pisub1mod[272]},${pisub2mod[272]},${pisub3mod[272]})&quot; -draw &quot;point 12,13&quot; \
-fill &quot;rgb(${pisub1mod[273]},${pisub2mod[273]},${pisub3mod[273]})&quot; -draw &quot;point 13,13&quot; \
-fill &quot;rgb(${pisub1mod[274]},${pisub2mod[274]},${pisub3mod[274]})&quot; -draw &quot;point 14,13&quot; \
-fill &quot;rgb(${pisub1mod[275]},${pisub2mod[275]},${pisub3mod[275]})&quot; -draw &quot;point 15,13&quot; \
-fill &quot;rgb(${pisub1mod[276]},${pisub2mod[276]},${pisub3mod[276]})&quot; -draw &quot;point 16,13&quot; \
-fill &quot;rgb(${pisub1mod[277]},${pisub2mod[277]},${pisub3mod[277]})&quot; -draw &quot;point 17,13&quot; \
-fill &quot;rgb(${pisub1mod[278]},${pisub2mod[278]},${pisub3mod[278]})&quot; -draw &quot;point 18,13&quot; \
-fill &quot;rgb(${pisub1mod[279]},${pisub2mod[279]},${pisub3mod[279]})&quot; -draw &quot;point 19,13&quot; \
-fill &quot;rgb(${pisub1mod[280]},${pisub2mod[280]},${pisub3mod[280]})&quot; -draw &quot;point 0,14&quot; \
-fill &quot;rgb(${pisub1mod[281]},${pisub2mod[281]},${pisub3mod[281]})&quot; -draw &quot;point 1,14&quot; \
-fill &quot;rgb(${pisub1mod[282]},${pisub2mod[282]},${pisub3mod[282]})&quot; -draw &quot;point 2,14&quot; \
-fill &quot;rgb(${pisub1mod[283]},${pisub2mod[283]},${pisub3mod[283]})&quot; -draw &quot;point 3,14&quot; \
-fill &quot;rgb(${pisub1mod[284]},${pisub2mod[284]},${pisub3mod[284]})&quot; -draw &quot;point 4,14&quot; \
-fill &quot;rgb(${pisub1mod[285]},${pisub2mod[285]},${pisub3mod[285]})&quot; -draw &quot;point 5,14&quot; \
-fill &quot;rgb(${pisub1mod[286]},${pisub2mod[286]},${pisub3mod[286]})&quot; -draw &quot;point 6,14&quot; \
-fill &quot;rgb(${pisub1mod[287]},${pisub2mod[287]},${pisub3mod[287]})&quot; -draw &quot;point 7,14&quot; \
-fill &quot;rgb(${pisub1mod[288]},${pisub2mod[288]},${pisub3mod[288]})&quot; -draw &quot;point 8,14&quot; \
-fill &quot;rgb(${pisub1mod[289]},${pisub2mod[289]},${pisub3mod[289]})&quot; -draw &quot;point 9,14&quot; \
-fill &quot;rgb(${pisub1mod[290]},${pisub2mod[290]},${pisub3mod[290]})&quot; -draw &quot;point 10,14&quot; \
-fill &quot;rgb(${pisub1mod[291]},${pisub2mod[291]},${pisub3mod[291]})&quot; -draw &quot;point 11,14&quot; \
-fill &quot;rgb(${pisub1mod[292]},${pisub2mod[292]},${pisub3mod[292]})&quot; -draw &quot;point 12,14&quot; \
-fill &quot;rgb(${pisub1mod[293]},${pisub2mod[293]},${pisub3mod[293]})&quot; -draw &quot;point 13,14&quot; \
-fill &quot;rgb(${pisub1mod[294]},${pisub2mod[294]},${pisub3mod[294]})&quot; -draw &quot;point 14,14&quot; \
-fill &quot;rgb(${pisub1mod[295]},${pisub2mod[295]},${pisub3mod[295]})&quot; -draw &quot;point 15,14&quot; \
-fill &quot;rgb(${pisub1mod[296]},${pisub2mod[296]},${pisub3mod[296]})&quot; -draw &quot;point 16,14&quot; \
-fill &quot;rgb(${pisub1mod[297]},${pisub2mod[297]},${pisub3mod[297]})&quot; -draw &quot;point 17,14&quot; \
-fill &quot;rgb(${pisub1mod[298]},${pisub2mod[298]},${pisub3mod[298]})&quot; -draw &quot;point 18,14&quot; \
-fill &quot;rgb(${pisub1mod[299]},${pisub2mod[299]},${pisub3mod[299]})&quot; -draw &quot;point 19,14&quot; \
-fill &quot;rgb(${pisub1mod[300]},${pisub2mod[300]},${pisub3mod[300]})&quot; -draw &quot;point 0,15&quot; \
-fill &quot;rgb(${pisub1mod[301]},${pisub2mod[301]},${pisub3mod[301]})&quot; -draw &quot;point 1,15&quot; \
-fill &quot;rgb(${pisub1mod[302]},${pisub2mod[302]},${pisub3mod[302]})&quot; -draw &quot;point 2,15&quot; \
-fill &quot;rgb(${pisub1mod[303]},${pisub2mod[303]},${pisub3mod[303]})&quot; -draw &quot;point 3,15&quot; \
-fill &quot;rgb(${pisub1mod[304]},${pisub2mod[304]},${pisub3mod[304]})&quot; -draw &quot;point 4,15&quot; \
-fill &quot;rgb(${pisub1mod[305]},${pisub2mod[305]},${pisub3mod[305]})&quot; -draw &quot;point 5,15&quot; \
-fill &quot;rgb(${pisub1mod[306]},${pisub2mod[306]},${pisub3mod[306]})&quot; -draw &quot;point 6,15&quot; \
-fill &quot;rgb(${pisub1mod[307]},${pisub2mod[307]},${pisub3mod[307]})&quot; -draw &quot;point 7,15&quot; \
-fill &quot;rgb(${pisub1mod[308]},${pisub2mod[308]},${pisub3mod[308]})&quot; -draw &quot;point 8,15&quot; \
-fill &quot;rgb(${pisub1mod[309]},${pisub2mod[309]},${pisub3mod[309]})&quot; -draw &quot;point 9,15&quot; \
-fill &quot;rgb(${pisub1mod[310]},${pisub2mod[310]},${pisub3mod[310]})&quot; -draw &quot;point 10,15&quot; \
-fill &quot;rgb(${pisub1mod[311]},${pisub2mod[311]},${pisub3mod[311]})&quot; -draw &quot;point 11,15&quot; \
-fill &quot;rgb(${pisub1mod[312]},${pisub2mod[312]},${pisub3mod[312]})&quot; -draw &quot;point 12,15&quot; \
-fill &quot;rgb(${pisub1mod[313]},${pisub2mod[313]},${pisub3mod[313]})&quot; -draw &quot;point 13,15&quot; \
-fill &quot;rgb(${pisub1mod[314]},${pisub2mod[314]},${pisub3mod[314]})&quot; -draw &quot;point 14,15&quot; \
-fill &quot;rgb(${pisub1mod[315]},${pisub2mod[315]},${pisub3mod[315]})&quot; -draw &quot;point 15,15&quot; \
-fill &quot;rgb(${pisub1mod[316]},${pisub2mod[316]},${pisub3mod[316]})&quot; -draw &quot;point 16,15&quot; \
-fill &quot;rgb(${pisub1mod[317]},${pisub2mod[317]},${pisub3mod[317]})&quot; -draw &quot;point 17,15&quot; \
-fill &quot;rgb(${pisub1mod[318]},${pisub2mod[318]},${pisub3mod[318]})&quot; -draw &quot;point 18,15&quot; \
-fill &quot;rgb(${pisub1mod[319]},${pisub2mod[319]},${pisub3mod[319]})&quot; -draw &quot;point 19,15&quot; \
-fill &quot;rgb(${pisub1mod[320]},${pisub2mod[320]},${pisub3mod[320]})&quot; -draw &quot;point 0,16&quot; \
-fill &quot;rgb(${pisub1mod[321]},${pisub2mod[321]},${pisub3mod[321]})&quot; -draw &quot;point 1,16&quot; \
-fill &quot;rgb(${pisub1mod[322]},${pisub2mod[322]},${pisub3mod[322]})&quot; -draw &quot;point 2,16&quot; \
-fill &quot;rgb(${pisub1mod[323]},${pisub2mod[323]},${pisub3mod[323]})&quot; -draw &quot;point 3,16&quot; \
-fill &quot;rgb(${pisub1mod[324]},${pisub2mod[324]},${pisub3mod[324]})&quot; -draw &quot;point 4,16&quot; \
-fill &quot;rgb(${pisub1mod[325]},${pisub2mod[325]},${pisub3mod[325]})&quot; -draw &quot;point 5,16&quot; \
-fill &quot;rgb(${pisub1mod[326]},${pisub2mod[326]},${pisub3mod[326]})&quot; -draw &quot;point 6,16&quot; \
-fill &quot;rgb(${pisub1mod[327]},${pisub2mod[327]},${pisub3mod[327]})&quot; -draw &quot;point 7,16&quot; \
-fill &quot;rgb(${pisub1mod[328]},${pisub2mod[328]},${pisub3mod[328]})&quot; -draw &quot;point 8,16&quot; \
-fill &quot;rgb(${pisub1mod[329]},${pisub2mod[329]},${pisub3mod[329]})&quot; -draw &quot;point 9,16&quot; \
-fill &quot;rgb(${pisub1mod[330]},${pisub2mod[330]},${pisub3mod[330]})&quot; -draw &quot;point 10,16&quot; \
-fill &quot;rgb(${pisub1mod[331]},${pisub2mod[331]},${pisub3mod[331]})&quot; -draw &quot;point 11,16&quot; \
-fill &quot;rgb(${pisub1mod[332]},${pisub2mod[332]},${pisub3mod[332]})&quot; -draw &quot;point 12,16&quot; \
-fill &quot;rgb(${pisub1mod[333]},${pisub2mod[333]},${pisub3mod[333]})&quot; -draw &quot;point 13,16&quot; \
-fill &quot;rgb(${pisub1mod[334]},${pisub2mod[334]},${pisub3mod[334]})&quot; -draw &quot;point 14,16&quot; \
-fill &quot;rgb(${pisub1mod[335]},${pisub2mod[335]},${pisub3mod[335]})&quot; -draw &quot;point 15,16&quot; \
-fill &quot;rgb(${pisub1mod[336]},${pisub2mod[336]},${pisub3mod[336]})&quot; -draw &quot;point 16,16&quot; \
-fill &quot;rgb(${pisub1mod[337]},${pisub2mod[337]},${pisub3mod[337]})&quot; -draw &quot;point 17,16&quot; \
-fill &quot;rgb(${pisub1mod[338]},${pisub2mod[338]},${pisub3mod[338]})&quot; -draw &quot;point 18,16&quot; \
-fill &quot;rgb(${pisub1mod[339]},${pisub2mod[339]},${pisub3mod[339]})&quot; -draw &quot;point 19,16&quot; \
-fill &quot;rgb(${pisub1mod[340]},${pisub2mod[340]},${pisub3mod[340]})&quot; -draw &quot;point 0,17&quot; \
-fill &quot;rgb(${pisub1mod[341]},${pisub2mod[341]},${pisub3mod[341]})&quot; -draw &quot;point 1,17&quot; \
-fill &quot;rgb(${pisub1mod[342]},${pisub2mod[342]},${pisub3mod[342]})&quot; -draw &quot;point 2,17&quot; \
-fill &quot;rgb(${pisub1mod[343]},${pisub2mod[343]},${pisub3mod[343]})&quot; -draw &quot;point 3,17&quot; \
-fill &quot;rgb(${pisub1mod[344]},${pisub2mod[344]},${pisub3mod[344]})&quot; -draw &quot;point 4,17&quot; \
-fill &quot;rgb(${pisub1mod[345]},${pisub2mod[345]},${pisub3mod[345]})&quot; -draw &quot;point 5,17&quot; \
-fill &quot;rgb(${pisub1mod[346]},${pisub2mod[346]},${pisub3mod[346]})&quot; -draw &quot;point 6,17&quot; \
-fill &quot;rgb(${pisub1mod[347]},${pisub2mod[347]},${pisub3mod[347]})&quot; -draw &quot;point 7,17&quot; \
-fill &quot;rgb(${pisub1mod[348]},${pisub2mod[348]},${pisub3mod[348]})&quot; -draw &quot;point 8,17&quot; \
-fill &quot;rgb(${pisub1mod[349]},${pisub2mod[349]},${pisub3mod[349]})&quot; -draw &quot;point 9,17&quot; \
-fill &quot;rgb(${pisub1mod[350]},${pisub2mod[350]},${pisub3mod[350]})&quot; -draw &quot;point 10,17&quot; \
-fill &quot;rgb(${pisub1mod[351]},${pisub2mod[351]},${pisub3mod[351]})&quot; -draw &quot;point 11,17&quot; \
-fill &quot;rgb(${pisub1mod[352]},${pisub2mod[352]},${pisub3mod[352]})&quot; -draw &quot;point 12,17&quot; \
-fill &quot;rgb(${pisub1mod[353]},${pisub2mod[353]},${pisub3mod[353]})&quot; -draw &quot;point 13,17&quot; \
-fill &quot;rgb(${pisub1mod[354]},${pisub2mod[354]},${pisub3mod[354]})&quot; -draw &quot;point 14,17&quot; \
-fill &quot;rgb(${pisub1mod[355]},${pisub2mod[355]},${pisub3mod[355]})&quot; -draw &quot;point 15,17&quot; \
-fill &quot;rgb(${pisub1mod[356]},${pisub2mod[356]},${pisub3mod[356]})&quot; -draw &quot;point 16,17&quot; \
-fill &quot;rgb(${pisub1mod[357]},${pisub2mod[357]},${pisub3mod[357]})&quot; -draw &quot;point 17,17&quot; \
-fill &quot;rgb(${pisub1mod[358]},${pisub2mod[358]},${pisub3mod[358]})&quot; -draw &quot;point 18,17&quot; \
-fill &quot;rgb(${pisub1mod[359]},${pisub2mod[359]},${pisub3mod[359]})&quot; -draw &quot;point 19,17&quot; \
-fill &quot;rgb(${pisub1mod[360]},${pisub2mod[360]},${pisub3mod[360]})&quot; -draw &quot;point 0,18&quot; \
-fill &quot;rgb(${pisub1mod[361]},${pisub2mod[361]},${pisub3mod[361]})&quot; -draw &quot;point 1,18&quot; \
-fill &quot;rgb(${pisub1mod[362]},${pisub2mod[362]},${pisub3mod[362]})&quot; -draw &quot;point 2,18&quot; \
-fill &quot;rgb(${pisub1mod[363]},${pisub2mod[363]},${pisub3mod[363]})&quot; -draw &quot;point 3,18&quot; \
-fill &quot;rgb(${pisub1mod[364]},${pisub2mod[364]},${pisub3mod[364]})&quot; -draw &quot;point 4,18&quot; \
-fill &quot;rgb(${pisub1mod[365]},${pisub2mod[365]},${pisub3mod[365]})&quot; -draw &quot;point 5,18&quot; \
-fill &quot;rgb(${pisub1mod[366]},${pisub2mod[366]},${pisub3mod[366]})&quot; -draw &quot;point 6,18&quot; \
-fill &quot;rgb(${pisub1mod[367]},${pisub2mod[367]},${pisub3mod[367]})&quot; -draw &quot;point 7,18&quot; \
-fill &quot;rgb(${pisub1mod[368]},${pisub2mod[368]},${pisub3mod[368]})&quot; -draw &quot;point 8,18&quot; \
-fill &quot;rgb(${pisub1mod[369]},${pisub2mod[369]},${pisub3mod[369]})&quot; -draw &quot;point 9,18&quot; \
-fill &quot;rgb(${pisub1mod[370]},${pisub2mod[370]},${pisub3mod[370]})&quot; -draw &quot;point 10,18&quot; \
-fill &quot;rgb(${pisub1mod[371]},${pisub2mod[371]},${pisub3mod[371]})&quot; -draw &quot;point 11,18&quot; \
-fill &quot;rgb(${pisub1mod[372]},${pisub2mod[372]},${pisub3mod[372]})&quot; -draw &quot;point 12,18&quot; \
-fill &quot;rgb(${pisub1mod[373]},${pisub2mod[373]},${pisub3mod[373]})&quot; -draw &quot;point 13,18&quot; \
-fill &quot;rgb(${pisub1mod[374]},${pisub2mod[374]},${pisub3mod[374]})&quot; -draw &quot;point 14,18&quot; \
-fill &quot;rgb(${pisub1mod[375]},${pisub2mod[375]},${pisub3mod[375]})&quot; -draw &quot;point 15,18&quot; \
-fill &quot;rgb(${pisub1mod[376]},${pisub2mod[376]},${pisub3mod[376]})&quot; -draw &quot;point 16,18&quot; \
-fill &quot;rgb(${pisub1mod[377]},${pisub2mod[377]},${pisub3mod[377]})&quot; -draw &quot;point 17,18&quot; \
-fill &quot;rgb(${pisub1mod[378]},${pisub2mod[378]},${pisub3mod[378]})&quot; -draw &quot;point 18,18&quot; \
-fill &quot;rgb(${pisub1mod[379]},${pisub2mod[379]},${pisub3mod[379]})&quot; -draw &quot;point 19,18&quot; \
-fill &quot;rgb(${pisub1mod[380]},${pisub2mod[380]},${pisub3mod[380]})&quot; -draw &quot;point 0,19&quot; \
-fill &quot;rgb(${pisub1mod[381]},${pisub2mod[381]},${pisub3mod[381]})&quot; -draw &quot;point 1,19&quot; \
-fill &quot;rgb(${pisub1mod[382]},${pisub2mod[382]},${pisub3mod[382]})&quot; -draw &quot;point 2,19&quot; \
-fill &quot;rgb(${pisub1mod[383]},${pisub2mod[383]},${pisub3mod[383]})&quot; -draw &quot;point 3,19&quot; \
-fill &quot;rgb(${pisub1mod[384]},${pisub2mod[384]},${pisub3mod[384]})&quot; -draw &quot;point 4,19&quot; \
-fill &quot;rgb(${pisub1mod[385]},${pisub2mod[385]},${pisub3mod[385]})&quot; -draw &quot;point 5,19&quot; \
-fill &quot;rgb(${pisub1mod[386]},${pisub2mod[386]},${pisub3mod[386]})&quot; -draw &quot;point 6,19&quot; \
-fill &quot;rgb(${pisub1mod[387]},${pisub2mod[387]},${pisub3mod[387]})&quot; -draw &quot;point 7,19&quot; \
-fill &quot;rgb(${pisub1mod[388]},${pisub2mod[388]},${pisub3mod[388]})&quot; -draw &quot;point 8,19&quot; \
-fill &quot;rgb(${pisub1mod[389]},${pisub2mod[389]},${pisub3mod[389]})&quot; -draw &quot;point 9,19&quot; \
-fill &quot;rgb(${pisub1mod[390]},${pisub2mod[390]},${pisub3mod[390]})&quot; -draw &quot;point 10,19&quot; \
-fill &quot;rgb(${pisub1mod[391]},${pisub2mod[391]},${pisub3mod[391]})&quot; -draw &quot;point 11,19&quot; \
-fill &quot;rgb(${pisub1mod[392]},${pisub2mod[392]},${pisub3mod[392]})&quot; -draw &quot;point 12,19&quot; \
-fill &quot;rgb(${pisub1mod[393]},${pisub2mod[393]},${pisub3mod[393]})&quot; -draw &quot;point 13,19&quot; \
-fill &quot;rgb(${pisub1mod[394]},${pisub2mod[394]},${pisub3mod[394]})&quot; -draw &quot;point 14,19&quot; \
-fill &quot;rgb(${pisub1mod[395]},${pisub2mod[395]},${pisub3mod[395]})&quot; -draw &quot;point 15,19&quot; \
-fill &quot;rgb(${pisub1mod[396]},${pisub2mod[396]},${pisub3mod[396]})&quot; -draw &quot;point 16,19&quot; \
-fill &quot;rgb(${pisub1mod[397]},${pisub2mod[397]},${pisub3mod[397]})&quot; -draw &quot;point 17,19&quot; \
-fill &quot;rgb(${pisub1mod[398]},${pisub2mod[398]},${pisub3mod[398]})&quot; -draw &quot;point 18,19&quot; \
-fill &quot;rgb(${pisub1mod[399]},${pisub2mod[399]},${pisub3mod[399]})&quot; -draw &quot;point 19,19&quot; \
-scale 400x400 draw_pi.png
[/bash]
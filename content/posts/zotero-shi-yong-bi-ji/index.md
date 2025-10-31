---
draft: false
---
﻿---
title: "Zotero浣跨敤绗旇"
date: 2022-11-21 16:13:02
---

## 鎻掍欢鎺ㄨ崘

鎻掍欢瀹夎姝ラ锛?

zotero棣栭〉鈫掑伐鍏封啋鎻掍欢鈫扞nstall Add-on From File鈫掍笂浼犳彃浠剁殑xpi鏂囦欢鈫掗噸鍚簲鐢ㄧ敓鏁?

*   DOI Manager

    *   鍔熻兘锛氳幏鍙栨枃鐚殑DOI鍙凤紝鍜孲CI-hub閰嶅悎鑾峰彇鏂囩尞鐨勫叏鏂噋df

    *   閾炬帴锛歔https://github.com/bwiernik/zotero-shortdoi](https://github.com/bwiernik/zotero-shortdoi "https://github.com/bwiernik/zotero-shortdoi")

    *   浣跨敤锛氬彸閿€夋嫨Manage DOIs->閫夋嫨Get long DOIs

        ![](./鏃犳爣棰榑MSGarro4z6.png "鍙抽敭閫夋嫨Manage DOIs->閫夋嫨Get long DOIs")

*   Zotero PDF Translate

    *   鍔熻兘锛歅DF缈昏瘧

    *   閾炬帴锛歔https://github.com/windingwind/zotero-pdf-translate](https://github.com/windingwind/zotero-pdf-translate "https://github.com/windingwind/zotero-pdf-translate")

    *   浣跨敤锛氬畨瑁呭悗锛岄€変腑pdf涓渶瑕佺炕璇戝瓧娈靛嵆鍙炕璇?

*   Zotero Scholar Rank & Zotero updateifsE

    *   鍔熻兘锛氭煡璇㈡枃鐚瓹CF鍜孲CI绛夌骇锛堟湁鏃跺€欐枃鐚嚜鍔ㄨ瘑鍒敊璇細瀵艰嚧鏌ヨ涓嶅噯锛?

    *   Zotero Scholar Rank閾炬帴锛歔https://github.com/SiriusXT/Zotero-Scholar-Rank](https://github.com/SiriusXT/Zotero-Scholar-Rank "https://github.com/SiriusXT/Zotero-Scholar-Rank")

    *   Zotero updateifsE閾炬帴锛歔https://github.com/redleafnew/zotero-updateifsE](https://github.com/redleafnew/zotero-updateifsE "https://github.com/redleafnew/zotero-updateifsE")

    *   浣跨敤锛氳瑙佹彃浠堕椤?

## 浣跨敤鎶€宸?

*   zotero Connector

    *   鍔熻兘锛氫竴娆綠oogle缃戦〉鎻掍欢锛屽彲浠ュ揩閫熷皢缃戦〉涓婄殑鏂囩尞涓嬭浇鍒皕otero锛堣嫢鏃犳硶鐩存帴鑾峰彇pdf锛屽彲浠ヤ娇鐢╠oi manager鍜宻ci hub閰嶅悎鑾峰彇pdf锛?

    *   浣跨敤锛氳胺姝孋hrome搴旂敤鍟嗗簵鎼滅储zotero Connector鈫掑湪鏂囩尞缃戦〉鍚姩鎻掍欢鈫掔偣鍑绘彃浠堕€夋嫨灏嗘枃鐚繚瀛樺埌鎸囧畾鐩綍涓?

        ![](./1669019185158.png)

*   SCI-hub璺緞閫夋嫨

    *   鍔熻兘锛歾otero鑾峰彇鍙敤pdf缁忓父鍑虹幇鎵句笉鍒扮殑鎯呭喌锛屽皢sci hub璺緞娣诲姞鍒皕otero涓紝澧炲ぇ鑾峰彇pdf鐨勬垚鍔熺巼锛?

    *   浣跨敤锛歾otero棣栭〉鈫掔紪杈戔啋棣栭€夐」鈫掗珮绾р啋楂樼骇璁剧疆鈫掕缃紪杈戝櫒鈫掓悳绱㈡杈撳叆"findpdf"鈫掔偣鍑绘浛鎹竴涓嬪唴瀹瑰埌杈撳叆妗嗏啋ok鈫掑浜庢病鏈塸df鐨勬枃鐚彸閿啋鎵惧埌鍙敤鐨刾df

        ```json
        { 
          "name":"sci-hub", 
          "method":"GET",    
          "url":"https://sci-hub.st/{doi}",    
          "mode":"html","selector":"#pdf",    
          "attribute":"src",
          "automatic":true
        }
        ```

        ![](./1669018079282_9nJpBUXqWu.png)

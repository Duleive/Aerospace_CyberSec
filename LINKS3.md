# Hack Fes 2026 「宇宙システムの攻防：事例分析とシミュレーションで学ぶ宇宙サイバーセキュリティ」

本講演に参加された方へ
期間限定で講演に使用した[スライド](HackFes2026_SAS_nonv.pdf)を公開します。ただし、念のため、私作成以外の画像は削除してあります。



- 宇宙サイバーセキュリティ勉強会
        - [宇宙サイバーセキュリティ勉強会](https://aerospace.connpass.com/)

- 講演中に現れたスライド(#Zero)
    - 衛星の軌道
        - [王立宇宙軍　オネアミスの翼](https://www.amazon.co.jp/dp/B01L7OXMOI)
        - [NORAD](https://ja.wikipedia.org/wiki/%E5%8C%97%E3%82%A2%E3%83%A1%E3%83%AA%E3%82%AB%E8%88%AA%E7%A9%BA%E5%AE%87%E5%AE%99%E9%98%B2%E8%A1%9B%E5%8F%B8%E4%BB%A4%E9%83%A8)
        - [CelesTrak](https://celestrak.org/NORAD/elements/)
		- [Two Line Element (TLE)の説明](https://gportal.jaxa.jp/gpr/assets/mng_upload/GCOM-C/TLE_ja.pdf)
        - [人工衛星・惑星探査機のための宇宙工学](https://amzn.asia/d/0c5fKgJR)

	- 衛星サービスのWebアプリケーション
    	- [気象衛星ひまわり](https://www.jma.go.jp/bosai/map.htm)
    	- [NOAA](https://www.noaa.gov/)
    	- [NOAA GOES](https://www.star.nesdis.noaa.gov/GOES/index.php)
        - [SatNOGS – Open Source global network of satellite ground](https://satnogs.org/)

	- 衛星追跡
    	- [N2YO](https://www.n2yo.com/)
    	- [satellite tracker3D](https://satellitetracker3d.com/)
    	- [NORAD(北アメリカ航空宇宙防衛司令部)](https://ja.wikipedia.org/wiki/%E5%8C%97%E3%82%A2%E3%83%A1%E3%83%AA%E3%82%AB%E8%88%AA%E7%A9%BA%E5%AE%87%E5%AE%99%E9%98%B2%E8%A1%9B%E5%8F%B8%E4%BB%A4%E9%83%A8)
    	- [CelesTrak](https://celestrak.org/)
 
 	- 過去のインシデント
        - [KA-SAT Network cyber attack overview](https://news.viasat.com/blog/corporate/ka-sat-network-cyber-attack-overview)
        - [名古屋港コンテナターミナルのサイバー攻撃におけるインシデント対応について](https://www.nisc.go.jp/pdf/policy/infra/shiryo2.pdf)
        - [キャプテン・ミッドナイト事件](https://en.wikipedia.org/wiki/Captain_Midnight_broadcast_signal_intrusion)
        - [Glitched on Earth by Humans: A Black-Box Security Evaluation of the SpaceX Starlink User Terminal](https://www.youtube.com/watch?v=NXqLMmGwJm0)

    - MITRE ATTACK/SPARTA
        - [MITRE att&ck framework](https://attack.mitre.org/)
        - [SPARTA](https://sparta.aerospace.org/)

    - 通信セグメント
        - [日本アマチュア無線連盟](https://www.jarl.org/index_1_hajimeru.html)    
        - [RTL-SDR](https://www.rtl-sdr.com/)    
        - [総務省Webページ 「陸上・海上航空分野の電波利用状況（周波数別利用状況一覧）」](https://www.soumu.go.jp/soutsu/chugoku/fieldinfo/denpa_ri_musen_riku_kai.html)    
        - [CCSDS SPACE DATA LINK SECURITY PROTOCOL](https://ccsds.org/Pubs/355x0b2.pdf)
        - [CCSDSPy](https://github.com/CCSDSPy/ccsdspy)

    - 衛星バスのシミュレーション
        - [NASA Operational Simulator for Space Systems (NOS3)](https://github.com/nasa/nos3)   
        - [YAMCS](https://yamcs.org/)    

	- 衛星追跡アプリケーション
        - [gpredict](https://github.com/csete/gpredict)
        - [SatDump](https://www.satdump.org/)        
        - [EPOCH](https://www.kratosspace.com/products/satellites/command-and-control/epoch-ips)     

	- 人工衛星シミュレーターNOS^3
        - [NASA Operational Simulator for Small Satellites (NOS^3)](https://software.nasa.gov/software/GSC-17737-1)
        - [GitHub Repo](https://github.com/nasa/nos3)
        - [Manual](https://nos3.readthedocs.io/en/latest/)

	- Install 
	- 以下のソフトウェアを使用します。ダウンロード・インストール（自己責任でお願いします）しておいてください。
        - [Oracle Virtual Box (Oracle VB)](https://www.virtualbox.org/)
        - [Vagrant](https://releases.hashicorp.com/vagrant/)
        - [Git on Windoes](https://git-scm.com/install/windows)

	- もし講師と全く同じにヴァージョンにしたい場合、以下の通りにダウンロードしてください。
        - [Oracle Virtual Box (Oracle VB) v7.0.18](https://www.virtualbox.org/wiki/Download_Old_Builds_7_0)
        - 下の方にスクロールして、VirtualBox 7.0.18 (released May 07 2024)​の下のWindows hostsをダブルクリックしてダウンロードします。
        - [Vagrant v2.4.1](https://releases.hashicorp.com/vagrant/2.4.1/)
        - CPUがAMDの場合は　vagrant_2.4.1_windows_amd64.msiをクリックしてダウンロードします。
        - [Gitはどのヴァージョンでも問題ありません。](https://git-scm.com/install/windows)

	- 宇宙サイバーセキュリティインシデント事例　p.14
        - [民間宇宙システムにおけるサイバーセキュリティ対策ガイドライン Ver 2.0(経産省)](https://www.meti.go.jp/shingikai/mono_info_service/sangyo_cyber/wg_seido/wg_uchu_sangyo/20240328_report.html)

	- 宇宙サイバーセキュリティの衛星
        - [Moonlighter](https://space.skyrocket.de/doc_sdat/moonlighter.htm)
        - [China Launches First-Generation 'Satellite Internet Firewall' Security Payload](https://uniteddaily.my/en/e763c987-6451-4bed-97dd-5bb0ac2bc801)

    - 参考文献
        - ["Cybersecurity for Space" (2024) ](https://link.springer.com/book/10.1007/979-8-8688-0339-0)
        - [いちから始める　Avionics Lesson](https://www.hobun-books.com/products/detail.php?product_id=275)
        - [電子戦の技術 基礎編](https://www.tdupress.jp/book/b349395.html)

    - 推奨する論文
        - [Space cybersecurity challenges, mitigation techniques, anticipated readiness, and future directions](https://www.sciencedirect.com/science/article/pii/S1874548224000659)
        - [dont look up there are sensitive internal links in the clear on geo satellites](https://satcom.sysnet.ucsd.edu/docs/dontlookup_ccs25_fullpaper.pdf)
        - [space Cyber security for low earth orbit satellite communications](https://www.cyber.gov.au/sites/default/files/2026-03/Securing%20space%20-%20Cyber%20Security%20for%20low%20earth%20orbit%20satellite%20communications.pdf)
        - [民間宇宙システムにおけるサイバーセキュリティ対策ガイドライン Ver 2.0(経産省)](https://www.meti.go.jp/shingikai/mono_info_service/sangyo_cyber/wg_seido/wg_uchu_sangyo/20240328_report.html)


	- 宇宙サイバーセキュリティ主要イベント  
        - [DEFCON](https://defcon.org/)
        - [DEFCON Aerospace Village](https://www.aerospacevillage.org/def-con-33/)
        - [CYSAT EUROPE 5/20-21](https://cysat.eu/cysat-europe/)
        - [CYSAT Youtube](https://www.youtube.com/@CYSAT)

	- 8月に行われる衛星CTF
        - [DEFCON USA Aug 6-9th LasVegas](https://defcon.org/)
        - [AEROSPACE VILLAGE STARPWN CTF Aug 6-9th LasVegas](https://starpwn.ctfd.io/)




```mermaid
graph TB

subgraph WAN
 Internet((Internet))
end

subgraph HOME[Y様邸]

 subgraph 2F
  direction LR

  subgraph ウォークインクローゼット
   direction LR
   Internet --> 211_2F_BBR[ブロードバンドルータ\n192.168.1.1]
  end

  subgraph 寝室
   direction LR
   211_2F_BBR --> 221_2F_HUB[HUB\n5ポート]
   221_2F_HUB --> 222_2F_TV[TV02]
   221_2F_HUB --> 223_2F_SV[サーバ01]
  end
 end

 subgraph 1F
  direction LR

  subgraph カウンター
   direction TB
   211_2F_BBR ----> 111_1F_HUB[mGig対応HUB]
   111_1F_HUB --> 112_1F_FS[mGig対応NAS\n192.168.1.45]
   113_1F_PTR[プリンター]
   114_1F_PC01[Surface Pro]
  end

  subgraph TVボード
   direction TB
   111_1F_HUB -----> 131_1F_AP02[AP02]
   131_1F_AP02 --x 132_1F_TV[TV01]
   131_1F_AP02 --> 133_1F_REC[レコーダー]
   132_1F_TV --HDMI--> 133_1F_REC
   134_1F_GAME[Nintendo\nSwitch]
   132_1F_TV --HDMI--> 134_1F_GAME
  end

  subgraph PCコーナー
   direction TB
   111_1F_HUB --> 121_1F_PoEHUB[PoE HUB]
   121_1F_PoEHUB --PoE--> 122_1F_AP01[AP01\nWiFi6]
   123_1F_PC02[Surface Go]
  end
  
  122_1F_AP01 -.-> 113_1F_PTR
  122_1F_AP01 -..-> 114_1F_PC01
  122_1F_AP01 -.-> 123_1F_PC02
  122_1F_AP01 -.-> 132_1F_TV
  122_1F_AP01 -..-> 134_1F_GAME
  122_1F_AP01 -..-> 101_SF01[iPhone01]
  122_1F_AP01 -...-> 102_SF02[iPhone02]
  122_1F_AP01 -...-> 103_SF03[Experia J9260]
  122_1F_AP01 -..-> 104_TB01[すみっコパッド]
  122_1F_AP01 -...-> 105_PC03[LIFEBOOK]
 end


end



classDef A fill:none,color:#0a0,stroke:#0a0

 classDef B fill :#E2730F,color: #FFF,%orange%
 classDef C fill :#FFFFFF,color: #000,%white%
 classDef D fill :#3E851D,color: #FFF,%green%
 classDef E fill :#D9105A,color: #FFF,%pink%
 classDef F fill :#7D48D9,color: #FFF,%purple%
 classDef G fill :#ffb469;
 
 classDef CP fill :#69ffb4;
 classDef OT fill :#b4ff69;


 ```
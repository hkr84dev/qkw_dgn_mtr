```mermaid
graph TB
 %% Groups
 classDef House fill:none,color:#0a0,stroke:#0a0
 classDef Floor fill:none,color:#59d,stroke:#59d,stroke-width:1px,stroke-dasharray:8
 classDef Room fill:#efe,color:#092,stroke:none

 %% Devices
 classDef NW fill:#84d,color:#fff,stroke:none
 classDef PC fill:#e83,color:#fff,stroke:none
 classDef SV fill:#493,color:#fff,stroke:#fff
 classDef Mobile fill:#46d,color:#fff,stroke:#fff
 classDef IoT fill:#aaa,color:#fff,stroke:#fff

 classDef B fill :#E2730F,color: #FFF,%orange%
 classDef C fill :#FFFFFF,color: #000,%white%
 classDef D fill :#3E851D,color: #FFF,%green%
 classDef E fill :#D9105A,color: #FFF,%pink%
 classDef F fill :#7D48D9,color: #FFF,%purple%
 classDef G fill :#ffb469;

 subgraph WAN
  direction TB
  Internet([Internet\nフレッツ 1Gbps])
  Internet --- 211_2F_BBR{{ブロードバンドルータ\n192.168.1.1}}
  class 211_2F_BBR NW

  subgraph Home[Y様邸]
   direction TB

   subgraph 2F
    direction LR

    subgraph ウォークインクローゼット
     direction LR
     211_2F_BBR
    end
    class ウォークインクローゼット Room

    subgraph 寝室
     direction LR
     211_2F_BBR --- 221_2F_HUB{{HUB\n5ポート}}
     221_2F_HUB --- 222_2F_TV[TV02]
     221_2F_HUB --- 223_2F_SV[(PRIMERGY)]
     class 221_2F_HUB NW
     class 222_2F_TV IoT
     class 223_2F_SV SV
    end
    class 寝室 Room

   end
   class 2F Floor

   subgraph 1F
    direction LR

    subgraph カウンター
     direction TB
     211_2F_BBR ----- 111_1F_HUB{{mGig対応HUB\n5ポート}}
     111_1F_HUB --- 112_1F_FS[(mGig対応NAS\n4TB RAID1\n192.168.1.45)]
     113_1F_PTR[プリンター]
     114_1F_PC01(Surface Pro)
     class 111_1F_HUB NW
     class 112_1F_FS SV
     class 113_1F_PTR IoT
     class 114_1F_PC01 PC
    end
    class カウンター Room

    subgraph PCコーナー
     direction TB
     111_1F_HUB --- 121_1F_PoEHUB{{PoE HUB}}
     121_1F_PoEHUB --PoE--- 122_1F_AP01{{AP01\nWiFi6}}
     121_1F_PoEHUB --- 123_1F_PC02[Surface Go]
     class 121_1F_PoEHUB NW
     class 122_1F_AP01 NW
     class 123_1F_PC02 PC
    end
    class PCコーナー Room

    subgraph TVボード
     direction TB
     111_1F_HUB ------ 131_1F_AP02{{AP02}}
     131_1F_AP02 --x 132_1F_TV[TV01]
     131_1F_AP02 --- 133_1F_REC[レコーダー]
     132_1F_TV --HDMI--- 133_1F_REC
     133_1F_REC --USB--- 134_1F_HDD[(3TB HDD)]
     135_1F_GAME[Nintendo\nSwitch]
     132_1F_TV --HDMI--- 135_1F_GAME
     class 131_1F_AP02 NW
     class 132_1F_TV IoT
     class 133_1F_REC IoT
     class 134_1F_HDD SV
     class 135_1F_GAME IoT
    end
    class TVボード Room
  
   %% 無線接続
   122_1F_AP01 -.- 113_1F_PTR
   122_1F_AP01 -..- 114_1F_PC01
   122_1F_AP01 -.- 123_1F_PC02
   122_1F_AP01 -.- 132_1F_TV
   122_1F_AP01 -.- 135_1F_GAME
   122_1F_AP01 -...- 101_SF01(iPhone01)
   122_1F_AP01 -....- 102_SF02(iPhone02)
   122_1F_AP01 -....- 103_SF03(Xperia J9260)
   122_1F_AP01 -...- 104_TB01(すみっコパッド)
   122_1F_AP01 -.....- 105_PC03(LIFEBOOK)
   class 101_SF01 Mobile
   class 102_SF02 Mobile
   class 103_SF03 Mobile
   class 104_TB01 Mobile
   class 105_PC03 PC
  end
  class 1F Floor

 end 
 class Home House

end
```

### 導入前課題と対応内容
1. おしゃれなテレワーク環境が欲しい
    * ディスプレー、モニターアームは白で統一
    * 配線カバー付きで見た目もスッキリ
1. Wi-Fiの電波が寝室まで届かない
    * PCコーナーのモニター背面にAPをマグネット設置
    * PoE給電で配線もスッキリ
    * TVボード内のAPはHUBとして再利用
1. ファイルサーバへのアクセスが遅い
    * mGig対応のNASとHUBを導入し、Cat6A配線でパフォーマンスを最大化
    * Wi-Fi6対応APにより高速アクセス
1. ファイルサーバの故障によりデータが損失する
    * NASをRAID1構成とすることで耐障害性を向上

### 部材（税抜定価）
* Wi-Fi6 AP
* PoE HUB
* 2.5Gbps対応NAS
* 2.5Gbps対応HUB
* ディスプレー
* モニターアーム
* マグネットシート
* ブックエンド
* Cat6A LANケーブル
  * 0.3m x 2
  * 0.5m x 1
  * 1.0m x 1
  * 2.0m x 1

### 作業工数（約3時間）
* 機器搬入、開梱：20 min
* モニターアーム、ディスプレー設置：40 min
* NAS、HUB設置：10 min
* PoE HUB、AP設置：10 min
* NAS初期設定：30 min
* AP初期設定：30 min
* 動作確認：20 min
* 後片付け：20 min
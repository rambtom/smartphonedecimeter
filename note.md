# Basics

OverView(DeepL)  

## コンペティションの目標
このコンペティションの目標は、スマートフォンの位置情報をデシメートルあるいはセンチメートルの解像度まで計算することです。これにより、HOVレーンのETA推定など、車線レベルの精度が必要なサービスを実現することができます。このコンペティションでは、ホストによって収集されたデータセットを使用して、オープンスカイや軽い都市道路で収集されたAndroidスマートフォンの生の位置測定に基づくモデルを開発します。  

あなたの仕事は、より細かい人間の行動の地理空間情報と粒度の改善されたモバイルインターネットとの間の接続を橋渡しし、より正確な位置を生成するのに役立つでしょう。その結果、より正確なデータをもとに、新しいナビゲーション手法が構築される可能性があります。  

## コンテキスト
高速道路の出口で車線変更に間に合わなかったことはありませんか？他のレーンではなく、カープールレーンの到着予定時刻（ETA）を知りたいと思ったことはないだろうか。これらやその他の便利な機能には、スマートフォンの正確な位置情報サービスが必要です。機械学習モデルは、全地球衛星測位システム（GNSS）データの精度を向上させることができます。より精度の高いデータがあれば、何十億というAndroid携帯のユーザーが、よりきめ細かな測位を体験できるようになるかもしれません。  

GNSSチップセットは生の測定値を提供し、それを使ってスマートフォンの位置を計算することができる。現在の携帯電話では、3～5メートルの測位精度しか得られません。高度なユースケースでは、この精度は十分ではなく、信頼性もありません。都市部の障害物は、GPSの精度に対する最大の障壁となります。この課題のデータには、オープンスカイと軽快な都市道路で収集されたトレースのみが含まれています。これらの高速道路や大通りは最も広く利用されている道路であり、スマートフォンの測位の限界が試されることになります。  

GoogleのAndroid GPSチームは、2021年に「Smartphone Decimeter Challenge」を開催しました。受賞者3名による作品は、ION GNSS+ 2021 Conferenceで発表されました。今年もナビゲーション学会との共催で、スマートフォンのGNSS測位精度の先進的な研究を求め、人々が自分の周りの世界をより良くナビゲートできるようにするためのコンペティションを開催します。昨年の成果を基に、本データには2021年大会のトレースも含まれています。  
  
今後のコンペティションでは、衛星信号の障害となる都市の奥地など、より過酷な環境で収集されたトレースも含まれる可能性があります。このコンペティションでの皆さんの取り組みが、このような難しいデータの解釈に影響を与えるかもしれません。デシメートルレベルの位置精度があれば、モバイルユーザーは、より優れた車線レベルのナビゲーション、AR歩行/運転、電話による正確な農業、交通安全問題の位置におけるより高い特異性を得ることができます。また、よりパーソナライズされた微調整されたナビゲーション体験が可能になります。  

# Data Description

OverView(DeepL)

このチャレンジでは、GPS衛星からの信号、加速度計の測定値、ジャイロスコープの測定値など、携帯電話の位置を特定するのに役立つさまざまな機器からデータを取得します。昨年のコンペティションと比較すると、全体的により多くのデータ、より多様なルート、そしてテストセット内の1ドライブにつき1台の携帯電話だけが表示されます。

このチャレンジのデザインは、レーンレベルマッピングのような後処理アプリケーションに焦点を当てているため、ルート上の将来のデータは、できるだけ正確に位置を生成するために利用できるようになります。一般的なGNSS測位アルゴリズムの開発を奨励するため、携帯電話内のGPSチップセット位置は、携帯電話のモデルやその他の要因によって異なるメーカー独自のアルゴリズムから得られるため、提供されません。

データ収集プロセスは、本論文で説明したものと同じコア・アプローチを使用しました。このデータセット/チャレンジに基づく作品を発表する場合は、コンペティション・ルールに従って適切な引用を行うようにしてください。


## [train/test]/[drive_id]/[phone_name]/device_gnss.csv 
各行は、生のGNSS測定値、派生値、ベースライン推定位置が含まれています。このベースラインは、各エポックの状態として、電話の位置（x、y、z）、クロックバイアス（t）、各ユニークな信号タイプのisrbMを使用して、標準の重み付き最小二乗（WLS）ソルバーで補正PrMと衛星位置を使用して計算されたものである。一部の生計測フィールドは、非推奨であるか、元の gnss_log.txt に入力されていないため、このファイルには含まれていません。  

MessageType - "Raw"，文の接頭辞．

utcTimeMillis - UTCエポック（1970/1/1）からのミリ秒、GnssClockから変換されたものです。

TimeNanos - GNSS受信機の内部ハードウェアクロックの値で、ナノ秒単位。

LeapSecond - クロックの時刻に関連付けられた閏秒。

FullBiasNanos - GPSレシーバー内部のハードウェアクロック(getTimeNanos())と1980年1月6日0000Zからの真のGPS時間との差、ナノ秒単位。

BiasNanos - クロックのサブナノ秒のバイアス。

BiasUncertaintyNanos - クロックのバイアスの不確かさ（1シグマ）、ナノ秒単位。

DriftNanosPerSecond - 1秒あたりのナノ秒単位のクロックのドリフト。

DriftUncertaintyNanosPerSecond - クロックのドリフトの不確かさ（1シグマ）、ナノ秒/秒。

HardwareClockDiscontinuityCount - ハードウェアクロックの不連続性の数。

Svid - 衛星ID。

TimeOffsetNanos - 測定が行われた時間オフセット（ナノ秒単位）。

State - 衛星との同期状態を表す整数。整数の各ビットは、測定の特定の状態情報の属性である。ビットと状態の対応については、 metadata/raw_state_bit_map.json ファイルを参照。

ReceivedSvTimeNanos - 測定時の受信GNSS衛星時刻、ナノ秒単位。

ReceivedSvTimeUncertaintyNanos - 受信したGNSS衛星時刻の誤差推定値（1シグマ）、ナノ秒単位で表示。

Cn0DbHz - キャリア対ノイズ密度（dB-Hz）。

PseudorangeRateMetersPerSecond - タイムスタンプでの擬似距離の速度、m/s単位で表示されます。

PseudorangeRateUncertaintyMetersPerSecond - m/s単位で表した疑似レンジのレートの不確かさ（1シグマ）です。

AccumulatedDeltaRangeState - '累積デルタレンジ'測定の状態を示す。整数の各ビットは、測定の状態に属性があります。ビットと状態の間のマッピングについては、metadata/accumulated_delta_range_state_bit_map.json ファイルを参照してください。

AccumulatedDeltaRangeMeters - 最後にチャンネルをリセットしてからの累積デルタレンジ、単位はメートル。

AccumulatedDeltaRangeUncertaintyMeters - 累積デルタレンジの不確かさ（1シグマ）、メーター単位。

CarrierFrequencyHz - 追従信号のキャリア周波数。

MultipathIndicator - イベントの'マルチパス'状態を示す値です。

ConstellationType - GNSSコンスタレーションタイプ。人間が読める値へのマッピングは metadata/constellation_type_mapping.csv ファイルで提供されます。

CodeType - GNSS 測定のコードタイプ。最近のログでのみ利用可能です。

ChipsetElapsedRealtimeNanos - システム起動以来、このクロックの経過したリアルタイム性をナノ秒単位で表したものです。最近のログでのみ利用可能です。

ArrivalTimeNanosSinceGpsEpoch - GPSエポック（1980/1/6 UTC深夜）以降のナノ秒の整数値です。この値は、Raw文に記述されたそれぞれのユニークなエポックに対して、round((Raw::TimeNanos - Raw::FullBiasNanos)) に等しくなります。

RawPseudorangeMeters - メートル単位の生の擬似距離。光速と、信号送信時間（receivedSvTimeInGpsNanos）から信号到着時間（Raw::TimeNanos - Raw::FullBiasNanos - Raw;;BiasNanos ）までの時間差との積です。その不確かさは、光速とReceivedSvTimeUncertaintyNanosの間の積で近似することができます。

SignalType - GNSS信号のタイプは、コンステレーション名と周波数帯の組み合わせです。スマートフォンで測定される一般的な信号タイプには、GPS_L1、GPS_L5、GAL_E1、GAL_E5A、GLO_G1、BDS_B1I、BDS_B1C、BDS_B2A、QZS_J1、およびQZS_J5が含まれています。

ReceivedSvTimeNanosSinceGpsEpoch - GPSエポックからナノ秒単位で、チップセットが受信した信号伝送時間。ReceivedSvTimeNanosから変換されたこの値は、すべての星座で統一された時間スケールで、ReceivedSvTimeNanosはGLONASSの場合は1日の時間、非GLONASS星座の場合は1週間の時間を参照しています。

SvPosition[X/Y/Z]EcefMeters - ttx = receivedSvTimeInGpsNanos - satClkBiasNanos（以下に定義）で定義される "真の信号送信時間 "の最良推定時のECEF座標フレーム内の衛星位置（メートル）。衛星放送のエフェメリスを使用して計算され、真の衛星位置に対して1m程度の誤差がある。

Sv[Elevation/Azimuth]Degrees - 衛星の仰角と方位を度数で表したもの。WLSで推定されたユーザ位置を用いて計算されます。

SvVelocity[X/Y/Z]EcefMetersPerSecond - "真の信号送信時間" ttxの最良推定値におけるECEF座標フレーム内の衛星速度（メートル毎秒）。衛星放送エフェメリスを使って、このアルゴリズムで計算される。

SvClockBiasMeters - 衛星時刻補正と、信号送信時刻（receivedSvTimeInGpsNanos）における衛星ハードウェア遅延をメートル単位で結合したものである。SatClkBiasNanosは、satelliteTimeCorrectionからsatelliteHardwareDelayを差し引いた値であり、その時間換算値はsatClkBiasNanosと呼ばれる。IS-GPS-200H 20.3.3.3.1 節に定義されているように、satelliteTimeCorrection は、∆tsv = af0 + af1(t - toc) + af2(t - toc)2 + ∆tr から求められ、satelliteHardwareDelay は 20.3.3.3.2 節に定義される。上記の式中のパラメータは、衛星放送エフェメリスに記載されている。

SvClockDriftMetersPerSecond - 信号送信時刻（receivedSvTimeInGpsNanos）における衛星クロックのドリフトをメートル毎秒で表し たものである。これは、t+0.5秒とt-0.5秒の衛星クロックバイアスの差に等しい。

IsrbMeters - 非GPS-L1信号からGPS-L1信号までの信号間距離バイアス（ISRB）（単位：m）。例えば、GPS L5のISRBMが1000mの場合、同じGPS衛星が送信するGPS L1疑似レンジよりもGPS L5疑似レンジの方が1000m長いことを意味する。GPS-L1信号の場合はゼロです。ISRBは、GPSチップセット・レベルで導入され、重み付き最小二乗エンジンの状態として推定されます。

IonosphericDelayMeters - 電離層遅延をメートル単位で表したもので、Klobucharモデルで推定されます。

TroposphericDelayMeters - Nigel Penna、Alan Dodson、W. Chen (2001)によるEGNOSモデルで推定された対流圏遅延（メートル単位）。

WlsPositionXEcefMeters - WlsPositionYEcefMeters,WlsPositionZEcefMeters: WLSソルバーによって推定されたECEF内のユーザー位置。


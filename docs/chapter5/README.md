# 5: 追加コンテンツ - センサーをつないでみる

早めに完了した人向けの追加コンテンツです。外部センサーを接続し、取得した値を送信してみます。

全てのセンサーを順に試す必要はありませんので、興味のあるセンサーから試してみてください。

## この章のゴール

- センサー接続の発展課題に取り組む
- 取得したセンサーデータを microcat1 から送信する
- 送信結果を Harvest で再確認する

今回利用するセンサーは、いずれもGroveという規格のコネクタを使用しているため、Grove コネクタを持つセンサーシールドやブレイクアウトボードを使用して接続することができます。例えばSORACOMのオンラインストアで販売されている「Wio BG770A」というマイコンはGroveコネクタを持っていて、このセンサー類を接続することが出来ます。

Micro.Cat1やRaspberry PiにはGroveコネクタがないため、今回はGroveをジャンパーピンに変換するケーブルを利用します。

## 1. 温湿度センサー

温湿度センサーを繋いでみましょう。

(センサーの写真)

Micro.Cat1の裏側(針のようなピンが並んでいる側)に、以下の3つを接続します。

- 3V3 (3.3V電源)
- GND (グラウンド)
- GPIO 16 (データ信号)

(接続の写真)

MicroPythonでは、GPIO 16のデジタルデータを取得することでデータを取得できます。以下のコードを貼り付けてみてください。

```python
import machine
import dht
import time

sensor = dht.DHT11(machine.Pin(16))  # DATA を GPIO16 に接続した場合

while True:
    try:
        sensor.measure()
        temp = sensor.temperature()
        hum = sensor.humidity()
        print("Temp:", temp, "C  Hum:", hum, "%")
    except OSError as e:
        print("Retrying..",e)
        time.sleep(1)
        continue

    time.sleep(2)
```

センサーが正しく動作していれば、コンソールに2秒ごとに温度と湿度が表示されます。センサー部分を指で暖めたりすると数値が変わるのが分かります。  
たまにセンサーがタイムアウトするため、それをtry-exceptでキャッチしてリトライするようにしています。

正常に取得できたら、chapter4のプログラムと組み合わせて、このデータをSORACOMへ送信してみましょう。


## 2. 距離センサー

超音波を使って物体までの距離を測定するセンサーを繋いでみましょう。

(センサーの写真)

Micro.Cat1の裏側(針のようなピンが並んでいる側)に、以下の3つを接続します。

- 3V3 (3.3V電源)
- GND (グラウンド)
- GPIO 15 (データ信号)

(接続の写真)

Raspberry Pi Picoで使う場合、トリガーバルスを送る必要があるので少しコードが煩雑になっています。

MicroPythonでは、GPIO 15にトリガーバルスを送って、その後エコー信号を受信することで距離を測定します。

以下のコードを貼り付けてみてください。

```python
from machine import Pin, time_pulse_us
import time

SIG_PIN = 15
sig = Pin(SIG_PIN, Pin.OUT)

def read_distance():
    # 1) トリガパルスを出す
    sig.init(Pin.OUT)
    sig.value(0)
    time.sleep_us(2)
    sig.value(1)
    time.sleep_us(10)
    sig.value(0)

    # 2) 入力に切り替えてエコーを待つ
    sig.init(Pin.IN)
    pulse = time_pulse_us(sig, 1, 30000)  # 最大30ms

    if pulse <= 0:
        return None

    # 3) パルス幅 → 距離（cm）
    distance_cm = pulse / 58.0
    return distance_cm

while True:
    d = read_distance()
    if d is None:
        print("no reading")
    else:
        print("distance:", d, "cm")
    time.sleep(0.2)
```

センサーの前に物体を置いてみて、表示されるセンサーの値が変わることを確認します。

正常に取得できたら、chapter4のプログラムと組み合わせて、このデータをSORACOMへ送信してみましょう。

---
- 次: [6: あとかたづけと注意事項](../chapter6/README.md)
- 前: [4: SORACOM へデータ送信して Harvest で確認](../chapter4/README.md)

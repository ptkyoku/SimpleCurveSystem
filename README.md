# SimpleCurveSystem
Simple Curve Systemを使用すると、画像のフェードや、オブジェクトの移動、回転、拡大、縮小などのアニメーションを簡単に作成できます。

## SimpleCurveSystemをUnityにインポート
- manifest.json に以下のコード追加すると、Unityライブラリに自動にインポートされて、使用できます。
```
"com.ptkyoku.simplecurvesystem":"https://github.com/ptkyoku/SimpleCurveSystem.git#v1.0.0"
```
## GameObjectにコンポーネント追加して利用
### コンポーネント一覧
- AlphaCurveAnimation (アニメーションターゲット：**Graphic**)
- CanvasAlphaCurveAnimation (アニメーションターゲット：**CanvasGroup**)
- PositionCurveAnimation (アニメーションターゲット：**Tranform**)
- RotationCurveAnimation (アニメーションターゲット：**Tranform**)
- ScaleCurveAnimation (アニメーションターゲット：**Tranform**)
- AlphaCurveAnimationArray (アニメーションターゲット：**Graphic[]**)
- PositionCurveAnimationArray (アニメーションターゲット：**Tranform[]**)
- RotationCurveAnimationArray (アニメーションターゲット：**Tranform[]**)
- ScaleCurveAnimationArray (アニメーションターゲット：**Tranform[]**)
![alphacurve](https://github.com/ptkyoku/SimpleCurveSystem/assets/21057634/9b03617b-0be5-46fc-a677-521bf8c562fc)

### LoopType には四種類があります
- One；アニメーション一回行う。
- Rebound：0 ～ 1 ～ 0 までのアニメーション一回行う。
- Loop：0 ～ 1 までのアニメーションをループする。
- Loop Rebound：ReBoundアニメーションをループする。

### EaseType
- Custom 自分で編集して、AnimationCurveを決めます。
- または、内部設定済みの AnimationCurveを選択します。
![easetype](https://github.com/ptkyoku/SimpleCurveSystem/assets/21057634/3162d561-112f-44a3-9df4-1d9f58dfe03e)

### Target
- アニメーションターゲットを指定します。
### PlayOnAwake
- PlayOnAwakeにチェック入れと、起動したら、すぐアニメーション開始ができます。
### PlayBackWard
- PlayBackWardにチェック入れと、逆再生ができます。
### OnStart
- アニメーション開始時に行うイベント
### OnComplete
- アニメーション終了時に行うイベント
### OnRebound
- LoopType(ReboundとLoop Rebound)時にのみ、行うイベント

## ソースコードで追加作成

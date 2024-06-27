# SimpleCurveSystem
Simple Curve Systemを使用すると、画像のフェードや、オブジェクトの移動、回転、拡大、縮小などのアニメーションを簡単に作成できます。

## SimpleCurveSystemをUnityにインポート
- manifest.json に以下のコード追加すると、Unityライブラリに自動にインポートされて、使用できます。
```
"com.ptkyoku.simplecurvesystem":"https://github.com/ptkyoku/SimpleCurveSystem.git#v1.0.0"
```
## GameObjectにコンポーネント追加して利用
![alphacurve](https://github.com/ptkyoku/SimpleCurveSystem/assets/21057634/9b03617b-0be5-46fc-a677-521bf8c562fc)

### コンポーネント一覧
- AlphaCurveAnimation：フェード　(アニメーションターゲット：**Graphic**)
- CanvasAlphaCurveAnimation：フェード　(アニメーションターゲット：**CanvasGroup**)
- PositionCurveAnimation：移動　(アニメーションターゲット：**Tranform**)
- RotationCurveAnimation：回転　(アニメーションターゲット：**Tranform**)
- ScaleCurveAnimation：拡大、縮小　(アニメーションターゲット：**Tranform**)
- AlphaCurveAnimationArray：フェード　(アニメーションターゲット：**Graphic[]**)
- PositionCurveAnimationArray：移動　(アニメーションターゲット：**Tranform[]**)
- RotationCurveAnimationArray：回転　(アニメーションターゲット：**Tranform[]**)
- ScaleCurveAnimationArray：拡大、縮小　(アニメーションターゲット：**Tranform[]**)

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

## ソースコードでアニメーション作成
### 参照 namespace
```
using SimpleCurveSystem;
```
### 画像のフェード
```
public Graphic target1, target2;
//一個のみ
target1.DoFade(1f, CurveEaseType.InLinear, 0f, CurveLoopType.Rebound).Play();
//複数同時に行う
this.DoFadeArray(1f, CurveEaseType.InLinear, 0f, CurveLoopType.Rebound, target1, target2).Play();
```
### オブジェクト移動
```
//一個のみ
transform.DoMove(new Vector3(100f, 100f, 0f), 1f, CurveEaseType.EaseOutBounce, 0f).Play();
//複数同時に行う
var infos = new CurveTargetInfo<Transform, Vector3>[]
{
    new CurveTargetInfo<Transform, Vector3>()
    {
        target = target1.transform,
        endValue = new Vector3(100f, 0f, 0f)
    },
    new CurveTargetInfo<Transform, Vector3>()
    {
    
        target = target2.transform,
        endValue = new Vector3(100f, 0f, 0f)
    }
};
this.DoMoveArray(0.5f, CurveEaseType.EaseInSine, 0f, CurveLoopType.Rebound, infos).Play();
```
### イベント追加
```
var player = this.DoCanvasFade(1f, CurveEaseType.InLinear, 0f, CurveLoopType.Rebound);
player.AddOnStartListener(() =>
{
    Debug.Log("Start");
});
player.AddOnReboundListener(() =>
{
    Debug.Log("Rebound");
});
player.AddOnCompleteListener(() =>
{
    Debug.Log("Complete");
});
player.Play();
```
### 逆再生
```
player.Play(true);
```
### コンポーネント解放
```
//アニメーション終わった時に解放させる。
player.Dispose();
```

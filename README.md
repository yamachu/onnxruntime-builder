# onnxruntime-builder
VOICEVOX COREで利用するonnxruntimeのビルドを行うリポジトリ

## ビルド

[`build`ワークフロー]をworkflow_dispatchで起動。
`WASM static libraryのみをビルドする`を有効にすると、既存のネイティブmatrixを実行せずWASMビルドだけを試せる。通常のビルドにWASMを追加する場合は、`WASM static libraryを追加でビルドする`を有効にする。成果物は`onnxruntime-wasm-static`（VOICEVOX版では`voicevox_onnxruntime-wasm-static`）artifactとして取得でき、初期構成はSIMD有効・threads無効。

## リリース

1. [`build`ワークフロー]を`release=true`で起動してdraft releaseを作成。
2. `WASM static libraryを追加でビルドする`を有効にして実行した場合は、`<target>-wasm-static-<version>.tgz`も同じreleaseに含まれる。

## 再リリース

1. リリースのときと同様、[`build`ワークフロー]を`release=true`で起動してdraft releaseを作成。
   補足: 作成したdraft releaseをブラウザで開くと、"Target"は"Tag"が指すコミット、すなわち古いリリースのコミットになってしまっているように見える。しかしそれはブラウザでの見た目のみであり、実際には`target_commitish`はちゃんと`tag_name`とは別個に設定されている。
2. 古いリリースをdraft化。
3. 古いタグを削除。
4. リリースのときと同様、releaseのdraftを解除する。
5. 問題なさそうであれば、2.でdraft化した古いリリースを削除する。

[`build`ワークフロー]: https://github.com/VOICEVOX/onnxruntime-builder/actions/workflows/build.yml

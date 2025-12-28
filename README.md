<iframe src="https://username.github.io/sarutahiko/" width="100%" height="600"></iframe># sarutahikosuhi
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>猿田彦数秘 計算ツール</title>
<style>
body { font-family: sans-serif; padding: 20px; }
input, button { font-size: 16px; padding: 5px; margin: 5px 0; }
.result { margin-top: 20px; }
</style>
</head>
<body>

<h2>猿田彦数秘 計算ツール</h2>
<label>名前を入力：</label>
<input type="text" id="nameInput" placeholder="例: tokitsuyoshi">
<br>
<button onclick="calculate()">計算する</button>

<div class="result" id="result"></div>

<script>
// モダン式
const modernMap = {
  A:1,B:2,C:3,D:4,E:5,F:6,G:7,H:8,I:9,J:1,K:2,L:3,M:4,N:5,O:6,P:7,Q:1,R:9,S:1,T:2,U:3,V:4,W:5,X:6,Y:7,Z:8
};

// カリオストロ式
const caliMap = {
  A:1,B:2,C:3,D:4,E:5,F:8,G:3,H:5,I:1,J:1,K:2,L:3,M:4,N:5,O:7,P:8,Q:1,R:2,S:3,T:4,U:6,V:6,W:6,X:6,Y:1,Z:7
};

// マスターナンバー
const masterNumbers = [11,22,33,38,47,56,65,74,83,92];

// 名前の文字ごとの合計
function sumName(name, map){
  let total = 0;
  for(let char of name){
    if(map[char]) total += map[char];
  }
  return total;
}

// 1桁 or マスターナンバー判定
function checkMaster(n){
  return masterNumbers.includes(n) ? `${n} (マスターナンバー)` : n;
}

function calculate(){
  const rawName = document.getElementById('nameInput').value.toUpperCase().replace(/[^A-Z]/g,'');
  if(!rawName){ alert("名前を入力してください"); return; }

  // モダン式
  const modernTotal = sumName(rawName, modernMap);
  const modernCore = sumName(rawName.replace(/[^AEIOU]/g,''), modernMap); // 母音だけ
  const modernPersona = modernTotal - modernCore; // 子音のみ
  const modernRoad = modernTotal;

  // カリオストロ式
  const caliTotal = sumName(rawName, caliMap);
  const caliCore = sumName(rawName.replace(/[^AEIOU]/g,''), caliMap);
  const caliPersona = caliTotal - caliCore;
  const caliRoad = caliTotal;

  // 猿田彦数秘（合算）
  const sarutahikoCore = modernCore + caliCore;
  const sarutahikoPersona = modernPersona + caliPersona;
  const sarutahikoRoad = modernRoad + caliRoad;

  const resultDiv = document.getElementById('result');
  resultDiv.innerHTML = `
    <b>モダン式:</b> コア: ${checkMaster(modernCore)}, ペルソナ: ${checkMaster(modernPersona)}, ロード: ${checkMaster(modernRoad)}<br>
    <b>カリオストロ式:</b> コア: ${checkMaster(caliCore)}, ペルソナ: ${checkMaster(caliPersona)}, ロード: ${checkMaster(caliRoad)}<br>
    <b>猿田彦数秘（合算）:</b> コア: ${checkMaster(sarutahikoCore)}, ペルソナ: ${checkMaster(sarutahikoPersona)}, ロード: ${checkMaster(sarutahikoRoad)}
  `;
}
</script>

</body>
</html>

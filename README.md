<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Nine-Box Matrix Storytelling Quiz</title>
<style>
  body { font-family: Arial, sans-serif; background:#f9fafb; margin:0; padding:20px; }
  h1 { text-align:center; }
  .card { background:#fff; border-radius:8px; padding:20px; margin:20px auto; max-width:800px; box-shadow:0 2px 6px rgba(0,0,0,0.1); }
  .choices { display:flex; flex-direction:column; gap:10px; margin-top:15px; }
  button.choice { padding:12px; border:none; border-radius:6px; cursor:pointer; font-size:15px; }
  button.choice:hover { opacity:0.9; }
  .grow { background:#10b981; color:#fff; }
  .select { background:#f59e0b; color:#fff; }
  .harvest { background:#ef4444; color:#fff; }
  .feedback { margin-top:15px; padding:12px; border-radius:6px; display:none; }
  .correct { background:#d1fae5; color:#065f46; }
  .wrong { background:#fee2e2; color:#991b1b; }
  .score { text-align:center; margin-top:20px; font-weight:bold; }
</style>
</head>
<body>
<h1>Nine-Box Matrix Strategy Quiz</h1>
<div class="card">
  <h2 id="title"></h2>
  <p id="desc"></p>
  <div class="choices">
    <button class="choice grow" data-choice="grow">Invest & Grow</button>
    <button class="choice select" data-choice="select">Selectivity & Earnings</button>
    <button class="choice harvest" data-choice="harvest">Harvest & Divest</button>
  </div>
  <div id="feedback" class="feedback">
    <div id="verdict"></div>
    <div id="explain"></div>
  </div>
  <div class="score">Question <span id="round">1</span>/10 | Score: <span id="score">0</span></div>
</div>

<script>
const cases = [
  {
    title:"Cloud SaaS in Hypergrowth",
    desc:"A startup offering developer collaboration tools has just signed a multi-year deal with AWS Marketplace. Their product is sticky, engineers are reluctant to switch, and retention is unusually high despite many competitors.",
    correct:"grow",
    rationale:"High attractiveness + strong strength → Invest & grow."
  },
  {
    title:"Steel Manufacturer in Policy Crossfire",
    desc:"A regional steel company is squeezed as government infrastructure spending falls and cheap imports flood the market. Buyers consolidate power, margins are razor-thin, and the firm has no unique technology.",
    correct:"harvest",
    rationale:"Low attractiveness + medium strength → Harvest & divest."
  },
  {
    title:"Diagnostics Chain Riding Preventive-Care Wave",
    desc:"A diagnostics company partners with hospitals to offer preventive health packages. Rising middle-class awareness and insurance coverage boost demand. Their labs are accredited and trusted, giving them strong referral advantages.",
    correct:"grow",
    rationale:"Medium attractiveness + high strength → Invest & grow."
  },
  {
    title:"Enterprise HR Software in Compliance Niche",
    desc:"A mid-sized HR software provider serves industries with strict labor compliance rules. Clients renew steadily, but expansion revenue is modest and engineering bandwidth is stretched thin.",
    correct:"select",
    rationale:"Medium attractiveness + medium strength → Selectivity & earnings."
  },
  {
    title:"Industrial Components Facing Substitution",
    desc:"A manufacturer of mechanical parts sees demand eroding as customers shift to cheaper 3D-printed substitutes. Large buyers negotiate aggressively, and the firm’s cost structure is inflexible.",
    correct:"harvest",
    rationale:"Low attractiveness + low strength → Harvest & divest."
  },
  {
    title:"Premium D2C Personal Care Brand",
    desc:"A skincare brand thrives on influencer marketing. Social commerce tailwinds are strong, but supply chain fragility and rising ad costs threaten margins. Repeat purchase rates vary widely.",
    correct:"grow",
    rationale:"High attractiveness + medium strength → Invest & grow."
  },
  {
    title:"Legacy Telecom Services",
    desc:"A telecom operator’s landline division still generates cash from corporate clients needing redundancy. However, mobile and VoIP alternatives dominate. The division has strong billing relationships but limited growth prospects.",
    correct:"select",
    rationale:"Low attractiveness + high strength → Selectivity & earnings."
  },
  {
    title:"Niche Luxury Fashion Label",
    desc:"A boutique fashion house sells handcrafted apparel at premium prices. Admired by a small loyal base, but struggles to scale beyond niche markets. Competitors replicate designs faster and cheaper.",
    correct:"harvest",
    rationale:"Medium attractiveness + low strength → Harvest & divest."
  },
  {
    title:"AI Logistics Optimizer",
    desc:"A logistics startup uses AI to cut delivery times for e-commerce giants. Their patented algorithms spread rapidly, and investors see this as a backbone technology for the next decade.",
    correct:"grow",
    rationale:"High attractiveness + high strength → Invest & grow."
  },
  {
    title:"Regional Retail Chain",
    desc:"A family-owned retail chain dominates in a few towns with loyal customers. Expansion is slow due to rising e-commerce penetration. Margins are steady, but growth is capped by geography.",
    correct:"select",
    rationale:"Medium attractiveness + medium strength → Selectivity & earnings."
  }
];

let idx=0, score=0;
const elTitle=document.getElementById("title");
const elDesc=document.getElementById("desc");
const elFeedback=document.getElementById("feedback");
const elVerdict=document.getElementById("verdict");
const elExplain=document.getElementById("explain");
const elRound=document.getElementById("round");
const elScore=document.getElementById("score");

function renderCase(){
  const c=cases[idx];
  elTitle.textContent=c.title;
  elDesc.textContent=c.desc;
  elFeedback.style.display="none";
  elRound.textContent=idx+1;
}

function choose(choice){
  const c=cases[idx];
  const isCorrect=choice===c.correct;
  elFeedback.style.display="block";
  elFeedback.className="feedback "+(isCorrect?"correct":"wrong");
  elVerdict.textContent=isCorrect?"Correct!":"Wrong.";
  elExplain.textContent=c.rationale;
  if(isCorrect) score++;
  elScore.textContent=score;
  setTimeout(nextCase,2000);
}

function nextCase(){
  idx++;
  if(idx<cases.length){
    renderCase();
  } else {
    elTitle.textContent="Quiz Complete!";
    elDesc.textContent=`Final Score: ${score}/${cases.length}`;
    document.querySelector(".choices").style.display="none";
    elFeedback.style.display="none";
  }
}

document.querySelectorAll(".choice").forEach(btn=>{
  btn.addEventListener("click",()=>choose(btn.dataset.choice));
});

renderCase();
</script>
</body>
</html>

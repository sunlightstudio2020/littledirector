// 動態讀取掃描結果
const allCards = [
  "01.老師.png",
  "02.獸醫.png",
  "03.牙醫.png",
  "05.藥劑師.png",
  "06.警察.png",
  "07.消防員.png",
  "08.郵差.png",
  "09.軍人.png",
  "11.美髮師.png",
  "12.公車司機.png",
  "13.空服員.png",
  "15.舞者.png",
  "16.直播主.png",
  "17.模特兒.png",
  "18.畫家.png",
  "19.音樂家.png",
  "20.作家.png",
  "22.YOUTUBER.png",
  "23.漫畫家.png",
  "24.演員.png",
  "25.科學家.png",
  "26.太空人.png",
  "27.農夫.png",
  "28.園藝師.png",
  "29.會計.png",
  "30.新聞記者.png",
  "31.攝影師.png",
  "32.棒球選手.png",
  "33.籃球員.png",
  "34.游泳選手.png",
  "35.足球員.png",
  "36.動物飼養員.png",
  "37.乒乓選手.png",
  "38.滑板好手.png",
  "39.政治人物:總統.png",
  "40.網球選手.png",
  "41.賽車手.png",
  "44.排球選手.png",
  "52.羽毛球選手.png",
  "71.高爾夫球高手.png",
  "72.自行車手.png",
  "73.跆拳道高手.png",
  "74.武術家.png",
  "75.保姆.png",
  "76.國標舞者.png",
  "77.昆蟲飼養員.png",
  "78.潛水教練.png",
  "79.航海員.png",
  "80.導遊.png",
];
let availableCards = [...allCards];

let intervalId = null;
let isShuffling = false;

const cardImg = document.getElementById("cardImage");
const cardName = document.getElementById("cardName");
const toggleBtn = document.getElementById("toggleBtn");
const shuffleSound = document.getElementById("shuffleSound");
const dingSound = document.getElementById("dingSound");

// 開始快速切換(洗牌, 100ms)
function startShuffle() {
  intervalId = setInterval(() => {
    if (availableCards.length === 0) {
      cardImg.src = "";
      cardName.textContent = "所有卡片都抽完囉！";
      return;
    }
    const rIdx = Math.floor(Math.random() * availableCards.length);
    const fileName = availableCards[rIdx];
    cardImg.src = "images/" + fileName;

    // 01.老師.png => split('.') => ["01","老師","png"]
    const parts = fileName.split('.');
    if (parts.length >= 3) {
      cardName.textContent = parts[1];
    } else {
      cardName.textContent = fileName;
    }
  }, 100);

  shuffleSound.currentTime = 0;
  shuffleSound.play();
}

// 停止洗牌 & 抽到卡片移除
function stopShuffle() {
  clearInterval(intervalId);
  shuffleSound.pause();
  shuffleSound.currentTime = 0;
  dingSound.play();

  if (availableCards.length === 0) {
    cardImg.src = "";
    cardName.textContent = "所有卡片都抽完囉！";
    return;
  }

  const rIdx = Math.floor(Math.random() * availableCards.length);
  const fileName = availableCards.splice(rIdx, 1)[0];
  cardImg.src = "images/" + fileName;

  const parts = fileName.split('.');
  if (parts.length >= 3) {
    cardName.textContent = parts[1];
  } else {
    cardName.textContent = fileName;
  }
}

function toggleDraw() {
  if (!isShuffling) {
    isShuffling = true;
    toggleBtn.textContent = "停止抽牌";
    startShuffle();
  } else {
    isShuffling = false;
    toggleBtn.textContent = "開始抽牌";
    stopShuffle();
  }
}

toggleBtn.addEventListener('click', toggleDraw);

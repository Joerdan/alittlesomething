// script.js

// --- Typewriter Animation ---
function animateText(element) {
  const originalText = element.getAttribute('data-original') || element.textContent;
  element.innerHTML = '';
  let delayCounter = 0;
  const words = originalText.split(' ');
  words.forEach((word, wordIndex) => {
    const wordSpan = document.createElement('span');
    wordSpan.style.whiteSpace = 'nowrap';
    for (let i = 0; i < word.length; i++) {
      const letterSpan = document.createElement('span');
      letterSpan.textContent = word[i];
      letterSpan.style.opacity = 0;
      letterSpan.style.display = 'inline-block';
      letterSpan.style.animation = 'fadeInUp 0.5s forwards';
      letterSpan.style.animationDelay = (delayCounter * 0.05) + 's';
      delayCounter++;
      wordSpan.appendChild(letterSpan);
    }
    element.appendChild(wordSpan);
    if (wordIndex < words.length - 1) {
      element.appendChild(document.createTextNode(' '));
      delayCounter++;
    }
  });
  return delayCounter * 0.05 + 0.5;
}

function animateContainer(container) {
  const texts = container.querySelectorAll('.animate-text');
  let maxDuration = 0;
  texts.forEach(text => {
    const duration = animateText(text);
    if (duration > maxDuration) maxDuration = duration;
  });
  const buttons = container.querySelectorAll('.delayed-button');
  setTimeout(() => {
    buttons.forEach(btn => {
      btn.style.opacity = 1;
      btn.style.pointerEvents = 'auto';
    });
  }, maxDuration * 1000);
}

function activateContainer(id) {
  document.querySelectorAll('.container').forEach(c => c.classList.remove('active'));
  const container = document.getElementById(id);
  container.classList.add('active');
  animateContainer(container);
}

// --- Navigation ---
document.getElementById('start').addEventListener('click', () => {
  activateContainer('step2');
});
document.getElementById('nextStep1').addEventListener('click', () => {
  activateContainer('step3');
});
document.getElementById('nextStep2').addEventListener('click', () => {
  activateContainer('step4');
  startHeartGame();
});

// --- Final Challenge Button (Step 5) ---
let finalClicks = 0;
document.getElementById('challengeBtn').addEventListener('click', (e) => {
  finalClicks++;
  const btn = e.target;
  btn.style.transition = 'transform 0.5s ease';
  if (finalClicks === 1) {
    btn.style.transform = 'translateX(100px)';
    btn.textContent = "lol too slow";
  } else if (finalClicks === 2) {
    btn.style.transform = 'translateX(-100px)';
    btn.textContent = "ALMOST got me";
  } else if (finalClicks === 3) {
    btn.style.transform = 'translateX(0)';
    activateContainer('step6');
  }
});

// --- Restart Button ---
document.getElementById('restart').addEventListener('click', () => {
  document.querySelectorAll('.container').forEach(c => c.classList.remove('active'));
  document.getElementById('gameContainer').innerHTML = '';
  score = 0;
  document.getElementById('scoreDisplay').textContent = "Score: 0/3";
  finalClicks = 0;
  const challengeBtn = document.getElementById('challengeBtn');
  if (challengeBtn) {
    challengeBtn.style.transform = '';
    challengeBtn.textContent = "Click Me";
  }
  activateContainer('step1');
});

// --- Interactive Hearts on Click ---
const heartEmojis = ["❤️", "💖", "💕", "💗", "💓", "💘", "💝", "💞"];
document.addEventListener('click', (e) => {
  if (e.target.closest('button')) return;
  const heart = document.createElement('span');
  heart.textContent = heartEmojis[Math.floor(Math.random() * heartEmojis.length)];
  heart.style.position = 'absolute';
  heart.style.left = (e.pageX - 10) + 'px';
  heart.style.top = (e.pageY - 10) + 'px';
  heart.style.fontSize = '24px';
  heart.style.opacity = 1;
  heart.style.pointerEvents = 'none';
  heart.style.transition = 'all 1s ease-out';
  document.body.appendChild(heart);
  setTimeout(() => {
    heart.style.top = (e.pageY - 50) + 'px';
    heart.style.opacity = 0;
  }, 10);
  setTimeout(() => { heart.remove(); }, 1010);
});

// --- Rose Petal Rain ---
function createPetal() {
  const petal = document.createElement('div');
  petal.textContent = '🌹';
  petal.className = 'petal';
  petal.style.left = Math.random() * 100 + '%';
  petal.style.fontSize = (Math.random() * 20 + 10) + 'px';
  const duration = Math.random() * 5 + 5;
  petal.style.animationDuration = duration + 's';
  petal.style.animationDelay = Math.random() * 5 + 's';
  document.getElementById('petal-container').appendChild(petal);
  setTimeout(() => { petal.remove(); }, (duration + parseFloat(petal.style.animationDelay)) * 1000);
}
setInterval(createPetal, 500);

// --- Heart Collector Game (Step 4) ---
let score = 0;
let gameInterval;
function startHeartGame() {
  score = 0;
  document.getElementById('scoreDisplay').textContent = "Score: 0/3";
  const gameContainer = document.getElementById('gameContainer');
  gameInterval = setInterval(() => {
    const heart = document.createElement('div');
    heart.textContent = '💖';
    heart.classList.add('game-heart');
    heart.style.left = Math.random() * (gameContainer.clientWidth - 30) + 'px';
    heart.style.top = Math.random() * (gameContainer.clientHeight - 30) + 'px';
    heart.style.fontSize = '2em';
    heart.style.cursor = 'pointer';
    heart.addEventListener('click', (e) => {
      e.stopPropagation();
      heart.remove();
      score++;
      document.getElementById('scoreDisplay').textContent = "Score: " + score + "/3";
      if (score >= 3) {
        clearInterval(gameInterval);
        console.log("Score reached 3!");
        setTimeout(() => {
          activateContainer('step5');
        }, 1000);
      }
    });
    gameContainer.appendChild(heart);
    setTimeout(() => {
      if (gameContainer.contains(heart)) heart.remove();
    }, 3000);
  }, 800);
}

// Scaphoid Clinical Decision Rule calculator
document.getElementById('calculateBtn').addEventListener('click', function () {
  const male = document.getElementById('male').checked ? 1 : 0;
  const snuffSwelling = document.getElementById('snuffSwelling').checked ? 1 : 0;
  const snuffPain = document.getElementById('snuffPain').checked ? 1 : 0;
  const ulnarPain = document.getElementById('ulnarPain').checked ? 1 : 0;
  const thumbPain = document.getElementById('thumbPain').checked ? 1 : 0;

  // Logistic regression formula provided
  const logit =
    (0.649662618 * male) +
    (0.51353467826 * snuffSwelling) +
    (-0.79038263985 * snuffPain) +
    (0.57681198857 * ulnarPain) +
    (0.66499549728 * thumbPain) -
    1.685;

  const probability = 1 / (1 + Math.exp(-logit));
  const percent = (probability * 100);
  const rounded = percent.toFixed(1);

  let message = `Probability of scaphoid fracture: ${rounded}%`;
  if (probability >= 0.15) {
    message += ' — Imaging indicated (≥ 15%).';
  } else {
    message += ' — Imaging not indicated (< 15%).';
  }

  document.getElementById('result').textContent = message;
});

// Register service worker for PWA caching if available
if ('serviceWorker' in navigator) {
  window.addEventListener('load', function () {
    navigator.serviceWorker.register('/service-worker.js').catch(function (err) {
      // console.warn('Service Worker registration failed:', err);
    });
  });
}

const MAX_TOKENS = 10;

const tokenData = [
  {
    name: 'BeatVerse',
    symbol: 'BTV',
    category: 'music',
    badge: 'Trending',
    price: '$2.84',
    change: '+8.1%',
    marketCap: '$18.4M',
    holders: '8.9K',
    supply: '6.5M',
    volume: '$1.2M',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #7ef9d4, #89b7ff)'
  },
  {
    name: 'GrooveChain',
    symbol: 'GROOVE',
    category: 'music',
    badge: 'Music',
    price: '$1.76',
    change: '+5.6%',
    marketCap: '$14.1M',
    holders: '7.4K',
    supply: '8M',
    volume: '$902K',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #ffd86b, #ff9b7a)'
  },
  {
    name: 'Melodia',
    symbol: 'MEL',
    category: 'music',
    badge: 'New',
    price: '$0.92',
    change: '+12.3%',
    marketCap: '$9.7M',
    holders: '4.2K',
    supply: '10.5M',
    volume: '$660K',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #a7d0ff, #d7b8ff)'
  },
  {
    name: 'SoundMint',
    symbol: 'SMT',
    category: 'music',
    badge: 'Popular',
    price: '$3.21',
    change: '+4.8%',
    marketCap: '$22.8M',
    holders: '9.3K',
    supply: '7.1M',
    volume: '$1.5M',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #7fe7d9, #8cc8ff)'
  },
  {
    name: 'PulseTone',
    symbol: 'PTN',
    category: 'music',
    badge: 'Music',
    price: '$1.12',
    change: '+6.4%',
    marketCap: '$12.5M',
    holders: '6.1K',
    supply: '11.2M',
    volume: '$710K',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #8cf2a8, #78d0ff)'
  },
  {
    name: 'RhythmX',
    symbol: 'RHYX',
    category: 'trending',
    badge: 'Trending',
    price: '$4.42',
    change: '+9.8%',
    marketCap: '$27.9M',
    holders: '11.8K',
    supply: '6.3M',
    volume: '$1.8M',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #fdf2a8, #ffb5d9)'
  },
  {
    name: 'VibeFund',
    symbol: 'VIB',
    category: 'new',
    badge: 'New',
    price: '$0.61',
    change: '+15.2%',
    marketCap: '$7.9M',
    holders: '3.2K',
    supply: '13M',
    volume: '$430K',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #8fe6ff, #73d5c4)'
  },
  {
    name: 'HarmonyMint',
    symbol: 'HMN',
    category: 'music',
    badge: 'Popular',
    price: '$1.94',
    change: '+3.9%',
    marketCap: '$16.8M',
    holders: '8.1K',
    supply: '8.6M',
    volume: '$980K',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #a8ffe8, #7db4ff)'
  },
  {
    name: 'NoteLedger',
    symbol: 'NTL',
    category: 'trending',
    badge: 'Trending',
    price: '$2.48',
    change: '+7.5%',
    marketCap: '$20.6M',
    holders: '9.7K',
    supply: '8.3M',
    volume: '$1.1M',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #ffd2a8, #ff95ca)'
  },
  {
    name: 'AudioNexus',
    symbol: 'ANX',
    category: 'music',
    badge: 'Music',
    price: '$1.43',
    change: '+6.7%',
    marketCap: '$13.3M',
    holders: '5.8K',
    supply: '9.3M',
    volume: '$840K',
    explorer: 'https://solscan.io',
    accent: 'linear-gradient(135deg, #cbb6ff, #7ce7d9)'
  }
];

const tokenGrid = document.getElementById('tokenGrid');
const walletButton = document.getElementById('walletButton');
const walletStatus = document.getElementById('walletStatus');
const tokenCount = document.getElementById('tokenCount');
const filterButtons = [...document.querySelectorAll('.filter-btn')];

let activeFilter = 'all';
let connectedWallet = null;

function renderTokens(filter = 'all') {
  const filteredTokens =
    filter === 'all'
      ? tokenData
      : tokenData.filter((token) => token.category === filter || token.badge.toLowerCase() === filter);

  const tokensToRender = filteredTokens.slice(0, MAX_TOKENS);

  tokenGrid.innerHTML = tokensToRender.length
    ? tokensToRender
        .map(
          (token) => `
            <article class="token-card">
              <div class="token-header">
                <div class="token-title-wrap">
                  <div class="token-thumb" style="background: ${token.accent};">${token.symbol.slice(0, 2)}</div>
                  <div>
                    <h3 class="token-name">${token.name}</h3>
                    <p class="token-symbol">${token.symbol}</p>
                  </div>
                </div>
                <span class="badge">${token.badge}</span>
              </div>

              <div class="token-price-row">
                <span class="price">${token.price}</span>
                <span class="change">${token.change}</span>
              </div>

              <div class="metric-list">
                <div><span>Market Cap</span><br><strong>${token.marketCap}</strong></div>
                <div><span>Holders</span><br><strong>${token.holders}</strong></div>
                <div><span>Supply</span><br><strong>${token.supply}</strong></div>
                <div><span>Volume</span><br><strong>${token.volume}</strong></div>
              </div>

              <div class="token-actions">
                <button class="action-btn" type="button">Buy</button>
                <a class="explorer-link" href="${token.explorer}" target="_blank" rel="noreferrer">View Explorer</a>
              </div>
            </article>
          `
        )
        .join('')
    : '<div class="empty-state">No tokens found for this selection.</div>';

  tokenCount.textContent = String(tokensToRender.length);
}

async function connectWallet() {
  if (!window.solana || !window.solana.isPhantom) {
    walletStatus.textContent = 'Phantom not installed';
    return;
  }

  try {
    const connection = new solanaWeb3.Connection(solanaWeb3.clusterApiUrl('mainnet-beta'));
    const response = await window.solana.connect();
    const publicKey = response.publicKey.toString();
    const balance = await connection.getBalance(response.publicKey);
    const solBalance = (balance / solanaWeb3.LAMPORTS_PER_SOL).toFixed(2);

    connectedWallet = publicKey;
    walletStatus.textContent = `${publicKey.slice(0, 6)}...${publicKey.slice(-4)} • ${solBalance} SOL`;
    walletButton.textContent = 'Wallet Connected';
  } catch (error) {
    walletStatus.textContent = 'Wallet connection failed';
    console.error(error);
  }
}

function setupFilters() {
  filterButtons.forEach((button) => {
    button.addEventListener('click', () => {
      filterButtons.forEach((btn) => btn.classList.toggle('active', btn === button));
      activeFilter = button.dataset.filter;
      renderTokens(activeFilter);
    });
  });
}

walletButton.addEventListener('click', async () => {
  if (connectedWallet) {
    await window.solana.disconnect();
    connectedWallet = null;
    walletButton.textContent = 'Connect Wallet';
    walletStatus.textContent = 'Wallet not connected';
    return;
  }

  await connectWallet();
});

renderTokens(activeFilter);
setupFilters();

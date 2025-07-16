# NairaConnect-App
Your digital finance hub for gift card trading, crypto conversion, and seamless bill payments in Nigeria.


G

Pinned chat

Conversation with Gemini
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>NairaConnect - Your Digital Finance Hub</title>

<script src="https://cdn.tailwindcss.com"></script>

<link rel="preconnect" href="https://fonts.googleapis.com">

<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">

<style>

body {

font-family: 'Inter', sans-serif;

background-color: #f8fafc;

color: #1f2937;

}

.container {

max-width: 1200px;

}

.btn-primary {

background-color: #059669;

color: white;

transition: background-color 0.3s ease-in-out;

}

.btn-primary:hover {

background-color: #047857;

}

.btn-secondary {

background-color: #fcd34d;

color: #1f2937;

transition: background-color 0.3s ease-in-out;

}

.btn-secondary:hover {

background-color: #fbbf24;

}

input[type="text"], input[type="number"], select, textarea {

border: 1px solid #d1d5db;

padding: 0.75rem;

border-radius: 0.5rem;

width: 100%;

box-sizing: border-box;

transition: border-color 0.2s ease-in-out;

}

input[type="text"]:focus, input[type="number"]:focus, select:focus, textarea:focus {

outline: none;

border-color: #059669;

box-shadow: 0 0 0 2px rgba(5, 150, 105, 0.2);

}

.card {

background-color: white;

border-radius: 0.75rem;

box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

padding: 1.5rem;

}

.loading-spinner {

border: 4px solid rgba(0, 0, 0, 0.1);

border-left-color: #059669;

border-radius: 50%;

width: 24px;

height: 24px;

animation: spin 1s linear infinite;

}

@keyframes spin {

0% { transform: rotate(0deg); }

100% { transform: rotate(360deg); }

}

</style>

</head>

<body class="min-h-screen flex flex-col">

<div id="root" class="flex-grow flex flex-col"></div>

<script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>

<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>

<script crossorigin src="https://unpkg.com/@babel/standalone@7.15.0/babel.min.js"></script>

<script type="text/babel">

const { useState, useEffect } = React;



async function callGeminiAPI(promptText) {

const apiKey = "";

const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

const payload = {

contents: [{ role: "user", parts: [{ text: promptText }] }]

};

try {

const response = await fetch(apiUrl, {

method: 'POST',

headers: { 'Content-Type': 'application/json' },

body: JSON.stringify(payload)

});

const result = await response.json();

if (result.candidates && result.candidates.length > 0 &&

result.candidates[0].content && result.candidates[0].content.parts &&

result.candidates[0].content.parts.length > 0) {

return result.candidates[0].content.parts[0].text;

} else {

console.error("Gemini API response structure unexpected:", result);

return "Error: Unexpected API response structure.";

}

} catch (error) {

console.error("Error calling Gemini API:", error);

return `Error: ${error.message}`;

}

}



function Header({ setActivePage }) {

return (

<header className="bg-white shadow-md sticky top-0 z-50">

<nav className="container mx-auto px-4 py-4 flex flex-col md:flex-row justify-between items-center">

<div className="flex items-center justify-between w-full md:w-auto mb-4 md:mb-0">

<h1 className="text-2xl font-bold text-gray-900">NairaConnect 🇳🇬</h1>

<button className="md:hidden text-gray-600 focus:outline-none">

<svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M4 6h16M4 12h16M4 18h16"></path></svg>

</button>

</div>

<div className="flex flex-col md:flex-row space-y-2 md:space-y-0 md:space-x-6 text-lg font-medium">

<button onClick={() => setActivePage('home')} className="text-gray-700 hover:text-green-600 transition-colors">Home</button>

<button onClick={() => setActivePage('giftcards')} className="text-gray-700 hover:text-green-600 transition-colors">Gift Cards</button>

<button onClick={() => setActivePage('crypto')} className="text-gray-700 hover:text-green-600 transition-colors">Crypto</button>

<button onClick={() => setActivePage('bills')} className="text-gray-700 hover:text-green-600 transition-colors">Bills</button>

<button onClick={() => setActivePage('referral')} className="text-gray-700 hover:text-green-600 transition-colors">Referral</button>

<button onClick={() => setActivePage('security')} className="text-gray-700 hover:text-green-600 transition-colors">Security</button>

<button onClick={() => setActivePage('support')} className="text-gray-700 hover:text-green-600 transition-colors">Support</button>

</div>

</nav>

</header>

);

}



function HomeSection() {

return (

<section className="py-16 bg-gradient-to-br from-green-50 to-emerald-100 text-center">

<div className="container mx-auto px-4">

<h2 className="text-4xl md:text-5xl font-bold text-gray-900 mb-6 leading-tight">

Your Trusted Partner for Digital Assets in Nigeria

</h2>

<p className="text-lg md:text-xl text-gray-700 mb-8 max-w-3xl mx-auto">

Trade gift cards, convert crypto, and pay bills seamlessly. Fast, Secure, and Reliable transactions, tailored for you.

</p>

<div className="flex flex-col sm:flex-row justify-center space-y-4 sm:space-y-0 sm:space-x-4">

<button className="btn-primary py-3 px-8 text-lg rounded-full shadow-lg">Get Started Now</button>

<button className="btn-secondary py-3 px-8 text-lg rounded-full shadow-lg">Learn More</button>

</div>

</div>

</section>

);

}



function GiftCardSection() {

const [cardType, setCardType] = useState('');

const [cardValue, setCardValue] = useState('');

const [estimatedRate, setEstimatedRate] = useState('Enter details to get an estimate.');

const [loading, setLoading] = useState(false);



const handleEstimateRate = async () => {

if (!cardType || !cardValue) {

setEstimatedRate('Please fill in both card type and value.');

return;

}

setLoading(true);

setEstimatedRate('Estimating...');

const prompt = `As a financial app for Nigerian users, provide an estimated Naira exchange rate for a ${cardType} gift card with a value of ${cardValue} USD. Assume current market conditions and factor in typical exchange fees. Provide only the estimated Naira amount and a brief disclaimer that it's an estimate.`;

const response = await callGeminiAPI(prompt);

setEstimatedRate(response);

setLoading(false);

};



return (

<section className="py-16">

<div className="container mx-auto px-4">

<h2 className="text-3xl font-bold text-center mb-8">Trade Your Gift Cards for Naira 💳</h2>

<p className="text-center text-gray-600 mb-12 max-w-2xl mx-auto">

Convert your unused gift cards from popular international brands into instant Naira. Get competitive rates and quick payouts.

</p>

<div className="card max-w-xl mx-auto p-6 md:p-8">

<div className="mb-6">

<label htmlFor="cardType" className="block text-gray-700 text-sm font-bold mb-2">Gift Card Type (e.g., Amazon, Steam, iTunes)</label>

<input

type="text"

id="cardType"

value={cardType}

onChange={(e) => setCardType(e.target.value)}

className="mb-4"

placeholder="e.g., Amazon"

/>

<label htmlFor="cardValue" className="block text-gray-700 text-sm font-bold mb-2">Gift Card Value (USD)</label>

<input

type="number"

id="cardValue"

value={cardValue}

onChange={(e) => setCardValue(e.target.value)}

className="mb-4"

placeholder="e.g., 50"

/>

</div>

<button onClick={handleEstimateRate} className="btn-secondary py-2 px-4 text-base rounded-md w-full mb-4 flex items-center justify-center">

{loading ? <div className="loading-spinner"></div> : 'Estimate Naira Rate'}

</button>

<div className="bg-gray-50 p-4 rounded-md text-center text-gray-800 font-semibold min-h-[60px] flex items-center justify-center">

{estimatedRate}

</div>

<button className="btn-primary py-2 px-4 text-base rounded-md w-full mt-6">Proceed to Sell Gift Card</button>

</div>

</div>

</section>

);

}



function CryptoSection() {

const [cryptoType, setCryptoType] = useState('BTC');

const [cryptoAmount, setCryptoAmount] = useState('');

const [trendSummary, setTrendSummary] = useState('Select a cryptocurrency and amount to get trend insights.');

const [loading, setLoading] = useState(false);



const handleGetTrend = async () => {

if (!cryptoType) {

setTrendSummary('Please select a cryptocurrency.');

return;

}

setLoading(true);

setTrendSummary('Fetching latest trends...');

const prompt = `As a financial app for Nigerian users, summarize recent price trends and key developments (2-3 sentences) for ${cryptoType}. Focus on information relevant to a user looking to buy or sell.`;

const response = await callGeminiAPI(prompt);

setTrendSummary(response);

setLoading(false);

};



return (

<section className="py-16 bg-gray-50">

<div className="container mx-auto px-4">

<h2 className="text-3xl font-bold text-center mb-8">Buy & Sell Crypto with Ease ₿</h2>

<p className="text-center text-gray-600 mb-12 max-w-2xl mx-auto">

Securely convert Bitcoin, Ethereum, USDT, and other cryptocurrencies to Naira, or buy crypto instantly.

</p>

<div className="card max-w-xl mx-auto p-6 md:p-8">

<div className="mb-6">

<label htmlFor="cryptoType" className="block text-gray-700 text-sm font-bold mb-2">Cryptocurrency</label>

<select

id="cryptoType"

value={cryptoType}

onChange={(e) => setCryptoType(e.target.value)}

className="mb-4"

>

<option value="BTC">Bitcoin (BTC)</option>

<option value="ETH">Ethereum (ETH)</option>

<option value="USDT">Tether (USDT)</option>

<option value="BNB">Binance Coin (BNB)</option>

</select>

<label htmlFor="cryptoAmount" className="block text-gray-700 text-sm font-bold mb-2">Amount</label>

<input

type="number"

id="cryptoAmount"

value={cryptoAmount}

onChange={(e) => setCryptoAmount(e.target.value)}

className="mb-4"

placeholder="e.g., 0.005"

/>

</div>

<button onClick={handleGetTrend} className="btn-secondary py-2 px-4 text-base rounded-md w-full mb-4 flex items-center justify-center">

{loading ? <div className="loading-spinner"></div> : 'Get Crypto Trend Insights'}

</button>

<div className="bg-gray-50 p-4 rounded-md text-center text-gray-800 font-semibold min-h-[80px] flex items-center justify-center">

{trendSummary}

</div>

<div className="flex space-x-4 mt-6">

<button className="btn-primary flex-1 py-2 px-4 text-base rounded-md">Buy Crypto</button>

<button className="btn-primary flex-1 py-2 px-4 text-base rounded-md">Sell Crypto</button>

</div>

</div>

</div>

</section>

);

}



function BillPaymentSection() {

const [billType, setBillType] = useState('');

const [accountNumber, setAccountNumber] = useState('');

const [billerSuggestions, setBillerSuggestions] = useState('Describe your bill for suggestions.');

const [loading, setLoading] = useState(false);



const handleSuggestBillers = async () => {

if (!billType) {

setBillerSuggestions('Please enter a bill type.');

return;

}

setLoading(true);

setBillerSuggestions('Generating suggestions...');

const prompt = `As a financial app for Nigerian users, suggest common biller categories or types of bills (e.g., electricity, airtime, data, cable TV) that users typically pay in Nigeria, based on the bill type "${billType}". Provide a list of 3-5 common examples.`;

const response = await callGeminiAPI(prompt);

setBillerSuggestions(response);

setLoading(false);

};



return (

<section className="py-16">

<div className="container mx-auto px-4">

<h2 className="text-3xl font-bold text-center mb-8">Seamless Bill Payments 💡</h2>

<p className="text-center text-gray-600 mb-12 max-w-2xl mx-auto">

Pay for electricity, airtime, data, cable TV, and more, directly from your app. Quick and convenient.

</p>

<div className="card max-w-xl mx-auto p-6 md:p-8">

<div className="mb-6">

<label htmlFor="billType" className="block text-gray-700 text-sm font-bold mb-2">Bill Type (e.g., Electricity, Airtime)</label>

<input

type="text"

id="billType"

value={billType}

onChange={(e) => setBillType(e.target.value)}

className="mb-

rentradar-ethiopia/
├── public/
│   ├── index.html
│   ├── app-screenshot.png
│   ├── google-play-badge.png
│   ├── app-store-badge.png
│   └── rentradar-social.jpg
├── src/
│   ├── components/
│   │   ├── ContactForm.tsx
│   │   └── SubscriptionForm.tsx
│   ├── firebase.ts
│   ├── utils/
│   │   └── analytics.ts
│   ├── App.tsx
│   ├── index.tsx
│   └── App.css
├── .env
└── package.json
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";

const firebaseConfig = {
  apiKey: process.env.REACT_APP_FIREBASE_API_KEY,
  authDomain: process.env.REACT_APP_FIREBASE_AUTH_DOMAIN,
  projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
  storageBucket: process.env.REACT_APP_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: process.env.REACT_APP_FIREBASE_MESSAGING_SENDER_ID,
  appId: process.env.REACT_APP_FIREBASE_APP_ID
};

const app = initializeApp(firebaseConfig);
export const db = getFirestore(app);
export const initGA = (trackingId: string) => {
  if (typeof window !== 'undefined' && !window.gtag) {
    const script = document.createElement('script');
    script.src = `https://www.googletagmanager.com/gtag/js?id=${trackingId}`;
    script.async = true;
    document.head.appendChild(script);

    window.dataLayer = window.dataLayer || [];
    window.gtag = function() {
      dataLayer.push(arguments);
    };
    gtag('js', new Date());
    gtag('config', trackingId);
  }
};

export const logPageView = (url?: string) => {
  gtag('event', 'page_view', {
    page_path: url || window.location.pathname
  });
};
/* Mobile Responsiveness */
@media (max-width: 768px) {
  .feature-grid { grid-template-columns: 1fr; }
  nav .flex { flex-direction: column; }
}

/* Accessibility */
button:focus, input:focus {
  outline: 2px solid #3b82f6;
  outline-offset: 2px;
}

/* Performance */
img { max-width: 100%; height: auto; }
npx create-react-app rentradar-ethiopia --template typescript
cd rentradar-ethiopia
npm install firebase react-router-dom formik yup @types/react-helmet
REACT_APP_FIREBASE_API_KEY=your_key
REACT_APP_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
REACT_APP_FIREBASE_PROJECT_ID=your_project_id
REACT_APP_FIREBASE_STORAGE_BUCKET=your_bucket.appspot.com
REACT_APP_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
REACT_APP_FIREBASE_APP_ID=your_app_id
npm install -g vercel
vercel

import React, { useState, useEffect, useCallback } from 'react';
import { initializeApp } from 'firebase/app';
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut, signInAnonymously } from 'firebase/auth';
import { getFirestore, doc, setDoc, getDoc, updateDoc, onSnapshot } from 'firebase/firestore';
import { Code, Bug, Plus, Star, User, LogIn, LogOut, X, BrainCircuit } from 'lucide-react';

// --- Firebase Configuration ---
// User's provided configuration is now integrated.
const firebaseConfig = {
  apiKey: "AIzaSyBeCfkiBYLUfk2QjEWmL_Uv_lv57FGsaK0",
  authDomain: "gen-lang-client-0352235929.firebaseapp.com",
  projectId: "gen-lang-client-0352235929",
  storageBucket: "gen-lang-client-0352235929.appspot.com",
  messagingSenderId: "984956149832",
  appId: "1:984956149832:web:f603678fbd8c55e507b87d",
  measurementId: "G-GRQQ0H3Y55"
};


// --- App ID ---
const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-code-bot-app';

// --- Initialize Firebase ---
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

// --- Gemini API Configuration ---
const GEMINI_API_KEY = "AIzaSyA7eRxE-hnVpmIlNFSc0sjz0SX3Ky2MwU8";
const GEMINI_API_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${GEMINI_API_KEY}`;

// --- Main App Component ---
export default function App() {
    const [page, setPage] = useState('generate');
    const [user, setUser] = useState(null);
    const [userData, setUserData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [isAuthModalOpen, setIsAuthModalOpen] = useState(false);

    // --- Authentication State Listener ---
    useEffect(() => {
        const unsubscribe = onAuthStateChanged(auth, (currentUser) => {
            if (currentUser) {
                // User is signed in (either normally or anonymously)
                setUser(currentUser);
                if (currentUser.isAnonymous) {
                    // Set default data for guest users
                    setUserData({
                        name: "Guest",
                        credits: { gc: 2, fc: 0, ac: 0 }
                    });
                    setLoading(false);
                } else {
                    // It's a registered user, so set up a real-time listener for their data from Firestore
                    const userDocRef = doc(db, "artifacts", appId, "users", currentUser.uid);
                    const unsubSnapshot = onSnapshot(userDocRef, (doc) => {
                        if (doc.exists()) {
                            setUserData(doc.data());
                        }
                        // Stop loading once we have a definitive answer about user data
                        setLoading(false);
                    });
                    return () => unsubSnapshot(); // Cleanup snapshot listener on unmount
                }
            } else {
                // User is not signed in at all. This happens on first load or after an explicit sign-out.
                // We'll attempt to sign them in anonymously to give them a guest session.
                signInAnonymously(auth).catch(error => {
                    console.error("Firebase Error: Anonymous sign-in failed. Please ensure it's enabled in your Firebase console.", error);
                    setLoading(false); // Stop loading even if auth fails
                });
            }
        });
        return () => unsubscribe(); // Cleanup auth listener on unmount
    }, []);
    
    const handleSignOut = async () => {
        await signOut(auth);
        // onAuthStateChanged will handle the rest by signing the user in anonymously
        setPage('generate');
    };

    if (loading) {
        return <div className="flex items-center justify-center h-screen bg-gray-900 text-white"><BrainCircuit className="animate-pulse h-16 w-16" /></div>;
    }

    return (
        <div className="min-h-screen bg-gray-900 text-gray-100 font-sans">
            <Navbar setPage={setPage} user={user} userData={userData} onSignOut={handleSignOut} onSignIn={() => setIsAuthModalOpen(true)} />
            <main className="p-4 md:p-8">
                <PageContent page={page} user={user} userData={userData} />
            </main>
            {isAuthModalOpen && <AuthModal onClose={() => setIsAuthModalOpen(false)} />}
        </div>
    );
}

// --- Navigation Component ---
function Navbar({ setPage, user, userData, onSignOut, onSignIn }) {
    const navItems = [
        { id: 'generate', icon: Code, label: 'Generate' },
        { id: 'fix', icon: Bug, label: 'Fix' },
        { id: 'add', icon: Plus, label: 'Add' },
        { id: 'challenges', icon: Star, label: 'Challenges' },
    ];

    return (
        <nav className="bg-gray-800/50 backdrop-blur-sm sticky top-0 z-50 p-4 flex justify-between items-center border-b border-gray-700">
            <div className="flex items-center gap-2">
                 <BrainCircuit className="h-8 w-8 text-blue-400" />
                 <span className="text-xl font-bold">CodeBot Helper</span>
            </div>
            <div className="hidden md:flex items-center gap-4">
                {navItems.map(item => (
                    <button key={item.id} onClick={() => setPage(item.id)} className="flex items-center gap-2 px-3 py-2 rounded-md hover:bg-gray-700 transition-colors">
                        <item.icon className="h-5 w-5" />
                        <span>{item.label}</span>
                    </button>
                ))}
            </div>
            <div className="flex items-center gap-4">
                {userData && (
                    <div className="flex gap-3 text-sm bg-gray-700/50 px-3 py-1.5 rounded-full">
                        <span>GC: {userData.credits?.gc ?? 0}</span>
                        <span>FC: {userData.credits?.fc ?? 0}</span>
                        <span>AC: {userData.credits?.ac ?? 0}</span>
                    </div>
                )}
                {user && !user.isAnonymous ? (
                    <div className="flex items-center gap-3">
                        <span className="hidden sm:inline">{userData?.name}</span>
                        <button onClick={onSignOut} className="p-2 rounded-full hover:bg-gray-700"><LogOut className="h-5 w-5" /></button>
                    </div>
                ) : (
                    <button onClick={onSignIn} className="flex items-center gap-2 px-3 py-2 rounded-md bg-blue-600 hover:bg-blue-700 transition-colors">
                        <LogIn className="h-5 w-5" />
                        <span>Sign Up / In</span>
                    </button>
                )}
            </div>
        </nav>
    );
}

// --- Page Content Router ---
function PageContent({ page, user, userData }) {
    switch (page) {
        case 'generate':
            return <GenerateCodePage user={user} userData={userData} />;
        case 'fix':
            return <FixCodePage user={user} userData={userData} />;
        case 'add':
            return <AddCodePage user={user} userData={userData} />;
        case 'challenges':
            return <ChallengesPage user={user} userData={userData} />;
        default:
            return <GenerateCodePage user={user} userData={userData} />;
    }
}

// --- API Call Helper ---
async function callGemini(prompt) {
    const payload = { contents: [{ role: "user", parts: [{ text: prompt }] }] };
    const response = await fetch(GEMINI_API_URL, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
    });
    if (!response.ok) {
        const errorBody = await response.json();
        console.error("Gemini API Error:", errorBody);
        throw new Error("API request failed.");
    }
    const result = await response.json();
    return result.candidates[0]?.content?.parts[0]?.text || "Sorry, I couldn't generate a response.";
}

// --- Credit Management Helper ---
async function updateUserCredits(userId, newCredits) {
    const userDocRef = doc(db, "artifacts", appId, "users", userId);
    await updateDoc(userDocRef, { credits: newCredits });
}

// --- Code Generation Page ---
function GenerateCodePage({ user, userData }) {
    const [prompt, setPrompt] = useState('');
    const [language, setLanguage] = useState('python');
    const [output, setOutput] = useState('');
    const [isLoading, setIsLoading] = useState(false);
    const [error, setError] = useState('');
    
    const handleGenerate = async () => {
        if (!prompt) {
            setError("Please enter a prompt.");
            return;
        }
        if (!user || !userData || userData.credits.gc < 1) {
            setError("You need at least 1 GC credit to generate code. Sign up or complete challenges to earn more!");
            return;
        }

        setIsLoading(true);
        setError('');
        setOutput('');

        try {
            const fullPrompt = `Generate a block of ${language} code based on the following prompt. Output only the raw code inside a markdown block, without any explanation. Prompt: "${prompt}"`;
            const result = await callGemini(fullPrompt);
            setOutput(result);
            
            // Deduct credit only for registered users, as guest credits are not persisted.
            if (!user.isAnonymous) {
                const newCredits = { ...userData.credits, gc: userData.credits.gc - 1 };
                await updateUserCredits(user.uid, newCredits);
            }

        } catch (e) {
            setError("Failed to generate code. Please try again.");
            console.error(e);
        } finally {
            setIsLoading(false);
        }
    };

    return (
        <div className="max-w-4xl mx-auto">
            <h1 className="text-3xl font-bold mb-4">Generate Code</h1>
            <p className="text-gray-400 mb-6">Describe the code you want to create. Our AI will generate it for you. Costs 1 GC.</p>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div className="flex flex-col gap-4">
                    <textarea value={prompt} onChange={e => setPrompt(e.target.value)} placeholder="e.g., A Python function that sorts a list of numbers" className="w-full h-40 p-3 bg-gray-800 border border-gray-700 rounded-md focus:ring-2 focus:ring-blue-500"></textarea>
                    <select value={language} onChange={e => setLanguage(e.target.value)} className="w-full p-3 bg-gray-800 border border-gray-700 rounded-md focus:ring-2 focus:ring-blue-500">
                        <option>python</option>
                        <option>javascript</option>
                        <option>html</option>
                        <option>css</option>
                        <option>java</option>
                    </select>
                    <button onClick={handleGenerate} disabled={isLoading} className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-md transition flex items-center justify-center gap-2 disabled:bg-gray-500">
                        {isLoading ? 'Generating...' : 'Generate'}
                    </button>
                    {error && <p className="text-red-400 mt-2">{error}</p>}
                </div>
                <div className="bg-gray-800 p-4 rounded-md min-h-[200px]">
                    <pre><code className={`language-${language}`}>{output}</code></pre>
                </div>
            </div>
        </div>
    );
}


// --- Code Fixing Page ---
function FixCodePage({ user, userData }) {
    const [code, setCode] = useState('');
    const [issue, setIssue] = useState('');
    const [output, setOutput] = useState('');
    const [isLoading, setIsLoading] = useState(false);
    const [error, setError] = useState('');

    const handleFix = async () => {
        if (!code) {
            setError("Please enter the code to fix.");
            return;
        }
        if (user.isAnonymous || !userData || userData.credits.fc < 1) {
            setError("You need to be signed in and have at least 1 FC credit to fix code.");
            return;
        }

        setIsLoading(true);
        setError('');
        setOutput('');

        try {
            const fullPrompt = `Fix the following code block. If a specific issue is described, focus on that. Otherwise, find and fix any bugs. Output only the corrected, raw code inside a markdown block. Original Code:\n\`\`\`\n${code}\n\`\`\`\n\nDescribed Issue: "${issue || 'No specific issue described, find general bugs.'}"`;
            const result = await callGemini(fullPrompt);
            setOutput(result);
            
            const newCredits = { ...userData.credits, fc: userData.credits.fc - 1 };
            await updateUserCredits(user.uid, newCredits);

        } catch (e) {
            setError("Failed to fix code. Please try again.");
            console.error(e);
        } finally {
            setIsLoading(false);
        }
    };
    
    return (
        <div className="max-w-4xl mx-auto">
            <h1 className="text-3xl font-bold mb-4">Fix My Code</h1>
            <p className="text-gray-400 mb-6">Paste your broken code and describe the issue. Our AI will fix it. Costs 1 FC.</p>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div className="flex flex-col gap-4">
                    <textarea value={code} onChange={e => setCode(e.target.value)} placeholder="Paste your broken code here..." className="w-full h-40 p-3 bg-gray-800 border border-gray-700 rounded-md"></textarea>
                    <textarea value={issue} onChange={e => setIssue(e.target.value)} placeholder="Optionally, describe what's wrong..." className="w-full h-20 p-3 bg-gray-800 border border-gray-700 rounded-md"></textarea>
                    <button onClick={handleFix} disabled={isLoading || user.isAnonymous} className="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-6 rounded-md transition disabled:bg-gray-500 disabled:cursor-not-allowed">
                        {isLoading ? 'Fixing...' : 'Fix Code'}
                    </button>
                    {error && <p className="text-red-400 mt-2">{error}</p>}
                </div>
                <div className="bg-gray-800 p-4 rounded-md min-h-[200px]">
                    <pre><code>{output}</code></pre>
                </div>
            </div>
        </div>
    );
}

// --- Add to Code Page ---
function AddCodePage({ user, userData }) {
    const [code, setCode] = useState('');
    const [request, setRequest] = useState('');
    const [output, setOutput] = useState('');
    const [isLoading, setIsLoading] = useState(false);
    const [error, setError] = useState('');

    const handleAdd = async () => {
        if (!code || !request) {
            setError("Please provide both the original code and the feature to add.");
            return;
        }
        if (user.isAnonymous || !userData || userData.credits.ac < 1) {
            setError("You need to be signed in and have at least 1 AC credit to add features.");
            return;
        }
        
        setIsLoading(true);
        setError('');
        setOutput('');
        
        try {
            const fullPrompt = `Add a feature to the following code block based on the given request. Output only the complete, updated, raw code inside a markdown block. Original Code:\n\`\`\`\n${code}\n\`\`\`\n\nRequest: "${request}"`;
            const result = await callGemini(fullPrompt);
            setOutput(result);
            
            const newCredits = { ...userData.credits, ac: userData.credits.ac - 1 };
            await updateUserCredits(user.uid, newCredits);

        } catch (e) {
            setError("Failed to add to code. Please try again.");
            console.error(e);
        } finally {
            setIsLoading(false);
        }
    };
    
    return (
        <div className="max-w-4xl mx-auto">
            <h1 className="text-3xl font-bold mb-4">Add to Code</h1>
            <p className="text-gray-400 mb-6">Paste your existing code and describe the new feature you want. Costs 1 AC.</p>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div className="flex flex-col gap-4">
                    <textarea value={code} onChange={e => setCode(e.target.value)} placeholder="Paste your original code here..." className="w-full h-40 p-3 bg-gray-800 border border-gray-700 rounded-md"></textarea>
                    <textarea value={request} onChange={e => setRequest(e.target.value)} placeholder="Describe the feature to add (e.g., 'Add a button that changes the background color')" className="w-full h-20 p-3 bg-gray-800 border border-gray-700 rounded-md"></textarea>
                    <button onClick={handleAdd} disabled={isLoading || user.isAnonymous} className="w-full bg-purple-600 hover:bg-purple-700 text-white font-bold py-3 px-6 rounded-md transition disabled:bg-gray-500 disabled:cursor-not-allowed">
                        {isLoading ? 'Adding...' : 'Add Feature'}
                    </button>
                    {error && <p className="text-red-400 mt-2">{error}</p>}
                </div>
                <div className="bg-gray-800 p-4 rounded-md min-h-[200px]">
                    <pre><code>{output}</code></pre>
                </div>
            </div>
        </div>
    );
}

// --- Challenges Page ---
function ChallengesPage({ user, userData }) {
    const [challenge, setChallenge] = useState(null);
    const [userSolution, setUserSolution] = useState('');
    const [feedback, setFeedback] = useState('');
    const [isLoading, setIsLoading] = useState(false);

    const challenges = [
        {
            id: 'python_calculator',
            title: 'Fix the Python Calculator',
            language: 'python',
            description: 'This simple calculator has a bug. Find it and fix it to earn 2 FC!',
            brokenCode: 'def calculate(a, b, op):\n  if op == "+":\n    return a - b # Bug is here!\n  elif op == "-":\n    return a + b # And here!\n  elif op == "*":\n    return a * b\n  elif op == "/":\n    return a / b\n  else:\n    return "Invalid operator"',
        },
    ];

    const selectChallenge = (c) => {
        setChallenge(c);
        setUserSolution(c.brokenCode);
        setFeedback('');
    };

    const handleSubmitSolution = async () => {
        if (!userSolution) return;
        if (user.isAnonymous) {
            setFeedback("You must be signed in to submit challenges.");
            return;
        }

        setIsLoading(true);
        setFeedback('');

        try {
            const prompt = `A user is trying to solve a coding challenge. Their goal is to fix the broken code. Compare their solution to the intended logic.
            Broken Code:\n\`\`\`${challenge.brokenCode}\`\`\`
            User's Solution:\n\`\`\`${userSolution}\`\`\`
            Is the user's solution a correct fix? Respond with "Correct!" if it is, and provide a brief explanation if it is not. A correct fix for the calculator involves swapping the '+' and '-' operations.`;
            
            const result = await callGemini(prompt);
            setFeedback(result);

            if (result.toLowerCase().includes('correct')) {
                const newCredits = { ...userData.credits, fc: userData.credits.fc + 2 };
                await updateUserCredits(user.uid, newCredits);
                setFeedback(result + "\n\nAwesome! 2 FC have been added to your account.");
            }

        } catch (e) {
            setFeedback("Error checking solution. Please try again.");
            console.error(e);
        } finally {
            setIsLoading(false);
        }
    };

    return (
        <div className="max-w-4xl mx-auto">
            <h1 className="text-3xl font-bold mb-4">Coding Challenges</h1>
            <p className="text-gray-400 mb-6">Complete challenges to earn free credits!</p>
            
            {!challenge ? (
                <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    {challenges.map(c => (
                        <div key={c.id} className="bg-gray-800 p-4 rounded-lg flex flex-col justify-between">
                            <div>
                                <h3 className="font-bold text-lg">{c.title}</h3>
                                <p className="text-sm text-gray-400 mt-2">{c.description}</p>
                            </div>
                            <button onClick={() => selectChallenge(c)} className="mt-4 w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md transition">
                                Start Challenge
                            </button>
                        </div>
                    ))}
                </div>
            ) : (
                <div>
                    <button onClick={() => setChallenge(null)} className="mb-4 text-blue-400 hover:underline">
                        &larr; Back to Challenges
                    </button>
                    <h2 className="text-2xl font-bold">{challenge.title}</h2>
                    <p className="text-gray-400 my-2">{challenge.description}</p>
                    <div className="grid grid-cols-1 md:grid-cols-2 gap-6 mt-4">
                        <textarea value={userSolution} onChange={e => setUserSolution(e.target.value)} className="w-full h-64 p-3 bg-gray-800 border border-gray-700 rounded-md font-mono"></textarea>
                        <div className="bg-gray-800 p-4 rounded-md">
                            <h3 className="font-bold mb-2">AI Feedback</h3>
                            <p className="text-sm whitespace-pre-wrap">{feedback}</p>
                        </div>
                    </div>
                    <button onClick={handleSubmitSolution} disabled={isLoading || user.isAnonymous} className="mt-4 w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-6 rounded-md transition disabled:bg-gray-500 disabled:cursor-not-allowed">
                        {isLoading ? 'Checking...' : 'Submit Solution'}
                    </button>
                </div>
            )}
        </div>
    );
}

// --- Authentication Modal ---
function AuthModal({ onClose }) {
    const [isLogin, setIsLogin] = useState(true);
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');
    const [name, setName] = useState('');
    const [error, setError] = useState('');

    const handleAuthAction = async (e) => {
        e.preventDefault();
        setError('');
        try {
            if (isLogin) {
                await signInWithEmailAndPassword(auth, email, password);
            } else {
                const userCredential = await createUserWithEmailAndPassword(auth, email, password);
                const user = userCredential.user;
                // Create user document in Firestore for the new user
                const userDocRef = doc(db, "artifacts", appId, "users", user.uid);
                await setDoc(userDocRef, {
                    name: name,
                    email: user.email,
                    credits: { gc: 2, fc: 2, ac: 2 }
                });
            }
            onClose();
        } catch (err) {
            setError(err.message);
        }
    };

    return (
        <div className="fixed inset-0 bg-black/60 flex items-center justify-center z-50">
            <div className="bg-gray-800 p-8 rounded-lg shadow-xl w-full max-w-md relative">
                <button onClick={onClose} className="absolute top-4 right-4 text-gray-400 hover:text-white"><X /></button>
                <h2 className="text-2xl font-bold text-center mb-4">{isLogin ? 'Log In' : 'Sign Up'}</h2>
                <form onSubmit={handleAuthAction}>
                    {!isLogin && (
                        <input type="text" placeholder="Name" value={name} onChange={e => setName(e.target.value)} className="w-full p-3 mb-4 bg-gray-700 border border-gray-600 rounded-md" required />
                    )}
                    <input type="email" placeholder="Email" value={email} onChange={e => setEmail(e.target.value)} className="w-full p-3 mb-4 bg-gray-700 border border-gray-600 rounded-md" required />
                    <input type="password" placeholder="Password" value={password} onChange={e => setPassword(e.target.value)} className="w-full p-3 mb-4 bg-gray-700 border border-gray-600 rounded-md" required />
                    {error && <p className="text-red-400 text-sm mb-4">{error}</p>}
                    <button type="submit" className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 rounded-md transition">
                        {isLogin ? 'Log In' : 'Create Account'}
                    </button>
                </form>
                <p className="text-center text-sm mt-4">
                    {isLogin ? "Don't have an account?" : "Already have an account?"}
                    <button onClick={() => setIsLogin(!isLogin)} className="text-blue-400 hover:underline ml-2">
                        {isLogin ? 'Sign Up' : 'Log In'}
                    </button>
                </p>
            </div>
        </div>
    );
}

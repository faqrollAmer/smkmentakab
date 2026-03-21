import React, { useState, useEffect, useMemo } from 'react';
import { initializeApp } from 'firebase/app';
import {
  getFirestore,
  collection,
  doc,
  setDoc,
  onSnapshot,
  updateDoc,
  deleteDoc,
  addDoc
} from 'firebase/firestore';
import {
  getAuth,
  signInAnonymously,
  signInWithCustomToken,
  onAuthStateChanged
} from 'firebase/auth';
import {
  CheckCircle,
  Clock,
  ChevronLeft,
  ChevronRight,
  Calendar,
  UploadCloud,
  X,
  Eye,
  ShieldCheck,
  Lock,
  UserCheck,
  FileText,
  Info,
  Trash2,
  Users,
  KeyRound,
  RefreshCw,
  Camera,
  Bell,
  BellRing,
  History,
  Download
} from 'lucide-react';

// --- KONFIGURASI & KONSTAN ---
const STAFF = [
  { id: 'pm1', name: "'Afifah Binti Abdul Aziz", category: 'makmal', role: 'Ketua Pembantu Makmal' },
  { id: 'pm2', name: 'Ida Zarina Binti Idris', category: 'makmal', role: 'Pembantu Makmal' },
  { id: 'pm3', name: 'Azian Binti Mohamad', category: 'makmal', role: 'Pembantu Makmal' },
  { id: 'pm4', name: 'Fatimah Binti Abdul Latiff', category: 'makmal', role: 'Pembantu Makmal' },
  { id: 'pm5', name: 'Zainun Binti Mohamed Ramthan', category: 'makmal', role: 'Pembantu Makmal' },
  { id: 'pm6', name: "Nor'aini Binti Md Yusoff", category: 'makmal', role: 'Pembantu Makmal' },
  { id: 'pm7', name: 'Fakarullah Amer Bin Zainal Abidin', category: 'makmal', role: 'Pembantu Makmal' },
  { id: 'pm8', name: 'Abdul Azam Bin Mohamed', category: 'makmal', role: 'Pembantu Makmal' },
  { id: 'pp1', name: 'Nor Faiza Binti Mustaffa Kamal', category: 'murid', role: 'PPM' },
  { id: 'pp2', name: 'Wan Azlena Binti Wan Deraman', category: 'murid', role: 'PPM' },
  { id: 'pp3', name: 'Mohd Faizal Bin Zainal', category: 'murid', role: 'PPM' },
  { id: 'pt1', name: 'Juhaida Binti Abd Rashid', category: 'tadbir', role: 'Ketua Pembantu Tadbir' },
  { id: 'pt2', name: 'Junainah Binti Hassan', category: 'tadbir', role: 'Pembantu Tadbir' },
  { id: 'pt3', name: 'Rafidah Binti Sidek', category: 'tadbir', role: 'Pembantu Tadbir' },
  { id: 'ka1', name: 'Muhammad Fahmi Bin Hamidin', category: 'am', role: 'PKA' },
  { id: 'ka2', name: 'Nursyaza Aina Binti Mohd Adaha', category: 'am', role: 'PKA' },
];

const CATEGORIES = {
  all: { label: 'Semua' },
  makmal: { label: 'Pembantu Makmal' },
  murid: { label: 'PPM' },
  tadbir: { label: 'Pembantu Tadbir' },
  am: { label: 'PKA' }
};

const CATEGORY_STYLES = {
  makmal: 'bg-violet-50 text-violet-600 border-violet-100',
  murid: 'bg-sky-50 text-sky-600 border-sky-100',
  tadbir: 'bg-teal-50 text-teal-600 border-teal-100',
  am: 'bg-orange-50 text-orange-600 border-orange-100'
};

const STATUS_STYLES = {
  verified: 'bg-emerald-50 text-emerald-600',
  submitted: 'bg-amber-50 text-amber-600',
  late: 'bg-rose-50 text-rose-600',
  none: 'bg-slate-50 text-slate-600'
};

// --- INITIALIZE FIREBASE ---
// Menggunakan pemboleh ubah persekitaran untuk membolehkan kod berjalan dalam pratonton.
// Apabila anda memuat naik ke Google Sites, pastikan anda menggantikan JSON.parse(__firebase_config) 
// dengan objek konfigurasi Firebase sebenar anda.
const firebaseConfig = typeof __firebase_config !== 'undefined' 
  ? JSON.parse(__firebase_config) 
  : {
      apiKey: "API_KEY_ANDA",
      authDomain: "PROJECT_ID_ANDA.firebaseapp.com",
      projectId: "PROJECT_ID_ANDA",
      storageBucket: "PROJECT_ID_ANDA.appspot.com",
      messagingSenderId: "SENDER_ID_ANDA",
      appId: "APP_ID_ANDA"
    };

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'smk-mentakab-tasks';

// --- UTILITI ---
const getWeekRange = (weekIndex) => {
  const year = new Date().getFullYear();
  let d = new Date(year, 0, 1);
  while (d.getDay() !== 1) d.setDate(d.getDate() + 1);
  d.setDate(d.getDate() + (weekIndex * 7));
  const monday = new Date(d);
  const friday = new Date(d);
  friday.setDate(friday.getDate() + 4);
  friday.setHours(23, 59, 59, 999);
  return { monday, friday, key: `${year}-W${weekIndex + 1}`, label: `Minggu ${weekIndex + 1}` };
};

const getCurrentWeekIndex = () => {
  const today = new Date();
  for (let i = 0; i < 52; i++) {
    const { monday, friday } = getWeekRange(i);
    const sunday = new Date(friday);
    sunday.setDate(sunday.getDate() + 2);
    if (today >= monday && today <= sunday) return i;
  }
  return 0;
};

const getInitials = (name) => {
  return name
    .split(' ')
    .map((n) => n[0])
    .filter((c) => /[A-Z]/.test(c))
    .slice(0, 2)
    .join('');
};

const getStatusMeta = (sub) => {
  if (!sub) return { label: 'Belum Hantar', className: STATUS_STYLES.none };
  if (sub.status === 'verified') return { label: 'Disahkan', className: STATUS_STYLES.verified };
  if (sub.is_late) return { label: 'Lewat', className: STATUS_STYLES.late };
  return { label: 'Dihantar', className: STATUS_STYLES.submitted };
};

// --- KOMPONEN CARTA PAI ---
const SimplePieChart = ({ verified, unsubmitted, late, total }) => {
  const safeTotal = total || 1;
  const radius = 20;
  const circumference = 2 * Math.PI * radius;
  const vPercent = (verified / safeTotal) * 100 || 0;
  const uPercent = (unsubmitted / safeTotal) * 100 || 0;
  const lPercent = (late / safeTotal) * 100 || 0;
  const vOffset = 0;
  const uOffset = (vPercent / 100) * circumference;
  const lOffset = ((vPercent + uPercent) / 100) * circumference;

  return (
    <div className="relative w-20 h-20 md:w-24 md:h-24 flex-shrink-0">
      <svg viewBox="0 0 50 50" className="transform -rotate-90 w-full h-full">
        <circle cx="25" cy="25" r={radius} fill="transparent" stroke="#f1f5f9" strokeWidth="8" />
        <circle cx="25" cy="25" r={radius} fill="transparent" stroke="#e11d48" strokeWidth="8" strokeDasharray={`${(lPercent / 100) * circumference} ${circumference}`} strokeDashoffset={-lOffset} strokeLinecap="round" />
        <circle cx="25" cy="25" r={radius} fill="transparent" stroke="#f59e0b" strokeWidth="8" strokeDasharray={`${(uPercent / 100) * circumference} ${circumference}`} strokeDashoffset={-uOffset} strokeLinecap="round" />
        <circle cx="25" cy="25" r={radius} fill="transparent" stroke="#10b981" strokeWidth="8" strokeDasharray={`${(vPercent / 100) * circumference} ${circumference}`} strokeDashoffset={-vOffset} strokeLinecap="round" />
      </svg>
      <div className="absolute inset-0 flex items-center justify-center">
        <span className="text-[10px] md:text-xs font-black text-[#1e3a5f]">{Math.round((verified/safeTotal)*100)}%</span>
      </div>
    </div>
  );
};

// --- KOMPONEN UTAMA ---
export default function App() {
  const [user, setUser] = useState(null);
  const [currentWeekIdx, setCurrentWeekIdx] = useState(getCurrentWeekIndex());
  const [activeTab, setActiveTab] = useState('all');
  const [submissions, setSubmissions] = useState([]);
  const [notifications, setNotifications] = useState([]);
  const [isAdmin, setIsAdmin] = useState(false);
  const [selectedStaff, setSelectedStaff] = useState(null);
  const [viewingFile, setViewingFile] = useState(null);
  const [statDetailModal, setStatDetailModal] = useState(null);
  const [toast, setToast] = useState(null);
  const [uploadData, setUploadData] = useState({ file: null, base64: null, mimeType: null });
  const [verifyNotes, setVerifyNotes] = useState('');
  const [isProcessing, setIsProcessing] = useState(false);
  const [schoolLogo, setSchoolLogo] = useState(null);
  const [showNotifPanel, setShowNotifPanel] = useState(false);
  const [showPasscodeModal, setShowPasscodeModal] = useState(false);
  const [passcodeInput, setPasscodeInput] = useState('');

  const currentWeek = useMemo(() => getWeekRange(currentWeekIdx), [currentWeekIdx]);

  // Auth Effect - Menangani kes pratonton dan luaran
  useEffect(() => {
    const initAuth = async () => {
      try {
        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
          await signInWithCustomToken(auth, __initial_auth_token);
        } else {
          await signInAnonymously(auth);
        }
      } catch (e) {
        console.error("Auth Error:", e);
      }
    };
    initAuth();
    return onAuthStateChanged(auth, setUser);
  }, []);

  // Firestore Sync Effect
  useEffect(() => {
    if (!user) return;

    const unsubSub = onSnapshot(collection(db, 'artifacts', appId, 'public', 'data', 'submissions'), (snap) => {
      setSubmissions(snap.docs.map(d => ({ id: d.id, ...d.data() })));
    }, (err) => console.error("Sub Snapshot Error:", err));

    const unsubSettings = onSnapshot(doc(db, 'artifacts', appId, 'public', 'data', 'settings', 'config'), (snap) => {
      if (snap.exists()) setSchoolLogo(snap.data().logo_url);
    });

    const unsubNotif = onSnapshot(collection(db, 'artifacts', appId, 'public', 'data', 'notifications'), (snap) => {
      const data = snap.docs.map(d => ({ id: d.id, ...d.data() }));
      setNotifications(data.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp)).slice(0, 15));
    });

    return () => { unsubSub(); unsubSettings(); unsubNotif(); };
  }, [user]);

  const showToast = (message, type = 'info') => {
    setToast({ message, type });
    setTimeout(() => setToast(null), 3000);
  };

  const logNotification = async (title, message, type = 'info') => {
    try {
      await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'notifications'), {
        title, message, type, timestamp: new Date().toISOString()
      });
    } catch (e) { console.error(e); }
  };

  const handleAdminToggle = () => {
    if (isAdmin) {
      setIsAdmin(false);
      showToast('Mod Pentadbir ditutup.', 'info');
    } else {
      setShowPasscodeModal(true);
      setPasscodeInput('');
    }
  };

  const submitPasscode = () => {
    if (passcodeInput === '1234') {
      setIsAdmin(true);
      setShowPasscodeModal(false);
      showToast('Akses Pengetua Disahkan.', 'success');
    } else if (passcodeInput === '0000') {
      setIsAdmin(true);
      setShowPasscodeModal(false);
      showToast('Akses Admin Disahkan.', 'success');
    } else {
      showToast('Kod salah.', 'error');
      setPasscodeInput('');
    }
  };

  const handleLogoChange = (e) => {
    if (!isAdmin) return;
    const file = e.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = async (event) => {
      await setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'settings', 'config'), {
        logo_url: event.target.result, updated_at: new Date().toISOString()
      }, { merge: true });
      showToast('Logo dikemaskini!', 'success');
    };
    reader.readAsDataURL(file);
  };

  const handleFileChange = (e) => {
    const file = e.target.files[0];
    if (!file || file.size > 1024 * 1024) {
      showToast('Maksimum fail 1MB.', 'error');
      return;
    }
    const reader = new FileReader();
    reader.onload = (event) => setUploadData({ 
      file, 
      base64: event.target.result,
      mimeType: file.type
    });
    reader.readAsDataURL(file);
  };

  const submitTask = async () => {
    if (!uploadData.base64 || !selectedStaff) return;
    setIsProcessing(true);
    const isLate = new Date() > currentWeek.friday;
    const docId = `${selectedStaff.id}_${currentWeek.key}`;
    const payload = {
      staff_id: selectedStaff.id, staff_name: selectedStaff.name,
      week_key: currentWeek.key, file_name: uploadData.file.name,
      file_data: uploadData.base64, 
      file_type: uploadData.mimeType,
      submitted_at: new Date().toISOString(),
      status: 'submitted', is_late: isLate, verified: false
    };

    try {
      await setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'submissions', docId), payload);
      await logNotification(
        isLate ? 'Penghantaran Lewat' : 'Tugasan Baru',
        `${selectedStaff.name} telah menghantar fail bagi ${currentWeek.label}.${isLate ? ' (Tindakan Lewat)' : ''}`,
        isLate ? 'warning' : 'success'
      );
      showToast(isLate ? 'Dihantar (Lewat).' : 'Berjaya dihantar!', 'success');
      setSelectedStaff(null);
      setUploadData({ file: null, base64: null, mimeType: null });
    } catch (err) { 
      console.error(err);
      showToast('Gagal.', 'error'); 
    }
    finally { setIsProcessing(false); }
  };

  const verifyTask = async (sub, status = 'verified') => {
    setIsProcessing(true);
    try {
      await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'submissions', sub.id), {
        status, verified: status === 'verified', verified_at: new Date().toISOString(), notes: verifyNotes
      });
      await logNotification('Tugasan Disahkan', `Tugasan ${sub.staff_name} bagi ${sub.week_key} telah disahkan oleh Pentadbir.`, 'info');
      showToast('Disahkan.', 'success');
      setSelectedStaff(null);
      setVerifyNotes('');
    } catch (err) { 
      console.error(err);
      showToast('Ralat.', 'error'); 
    }
    finally { setIsProcessing(false); }
  };

  const deleteTask = async (submissionId) => {
    if (!isAdmin) return;
    setIsProcessing(true);
    try {
      await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'submissions', submissionId));
      await logNotification('Tugasan Dipadam', 'Rekod tugasan telah dipadam oleh Pentadbir.', 'warning');
      showToast('Rekod dipadam.', 'success');
      setSelectedStaff(null);
    } catch (err) {
      console.error(err);
      showToast('Gagal padam.', 'error');
    } finally {
      setIsProcessing(false);
    }
  };

  const stats = useMemo(() => {
    const weekSubs = submissions.filter(s => s.week_key === currentWeek.key);
    const verifiedList = STAFF.filter(st => weekSubs.find(s => s.staff_id === st.id && s.status === 'verified'));
    const unsubmittedList = STAFF.filter(st => !weekSubs.find(s => s.staff_id === st.id));
    const lateList = STAFF.filter(st => weekSubs.find(s => s.staff_id === st.id && s.is_late));
    return {
      total: { label: 'Jumlah Staf', value: STAFF.length, list: STAFF, color: 'slate' },
      verified: { label: 'Disahkan', value: verifiedList.length, list: verifiedList, color: 'emerald' },
      unsubmitted: { label: 'Belum Hantar', value: unsubmittedList.length, list: unsubmittedList, color: 'amber' },
      late: { label: 'Lewat', value: lateList.length, list: lateList, color: 'rose' }
    };
  }, [submissions, currentWeek.key]);

  const filteredStaff = STAFF.filter(s => activeTab === 'all' || s.category === activeTab);

  return (
    <div className="min-h-screen bg-slate-50 font-sans text-slate-900 pb-20">
      {/* Header Utama */}
      <header className="bg-gradient-to-br from-[#1e3a5f] to-[#0c2340] text-white p-6 md:p-10 relative overflow-hidden">
        <div className="absolute top-0 right-0 w-96 h-96 bg-blue-400/10 rounded-full -mr-32 -mt-32 blur-3xl" />
        <div className="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-8 relative z-10">
          <div className="flex items-center gap-6">
            <div className="relative group">
              <div className="w-20 h-20 md:w-24 md:h-24 bg-white rounded-[2rem] flex items-center justify-center shadow-2xl border-4 border-white/20 overflow-hidden transition-transform group-hover:scale-105">
                {schoolLogo ? <img src={schoolLogo} alt="Logo" className="w-full h-full object-contain" /> : <span className="text-2xl font-black text-[#1e3a5f]">SMK</span>}
              </div>
              {isAdmin && (
                <button onClick={() => document.getElementById('logo-upload').click()} className="absolute -bottom-2 -right-2 bg-amber-500 p-2.5 rounded-full shadow-lg border-2 border-white hover:bg-amber-600 transition-all">
                  <Camera className="w-4 h-4 text-white" />
                  <input id="logo-upload" type="file" hidden accept="image/*" onChange={handleLogoChange} />
                </button>
              )}
            </div>
            <div className="flex-1">
              <h1 className="text-lg md:text-2xl lg:text-3xl font-black tracking-tight uppercase leading-none md:whitespace-nowrap">Rekod Penghantaran Senarai Tugas Harian</h1>
              <p className="text-blue-300 text-xs md:text-sm font-black tracking-[0.2em] uppercase mt-0.5">Sekolah Menengah Kebangsaan Mentakab</p>
              <div className="flex items-center gap-2 mt-1 text-[10px] md:text-xs text-amber-300 font-bold bg-white/10 px-4 py-1.5 rounded-full border border-white/10 w-fit">
                <ShieldCheck className="w-4 h-4" /> Pengetua: Hajah Aniza Binti Baharuddin
              </div>
            </div>
          </div>

          <div className="flex flex-col items-center md:items-end gap-4">
            <div className="flex items-center gap-3">
              <button onClick={() => setShowNotifPanel(true)} className="p-4 rounded-2xl transition-all border flex items-center justify-center relative bg-white/10 border-white/20 hover:bg-white/20 shadow-lg">
                {notifications.length > 0 ? (
                  <>
                    <BellRing className="w-6 h-6 text-amber-400 animate-pulse" />
                    <span className="absolute -top-1 -right-1 w-5 h-5 bg-red-600 text-white text-[10px] font-black flex items-center justify-center rounded-full border-2 border-[#0c2340]">
                      {notifications.length}
                    </span>
                  </>
                ) : <Bell className="w-6 h-6 text-white/50" />}
              </button>

              <button onClick={handleAdminToggle} className={`flex items-center gap-3 px-6 py-4 rounded-2xl text-sm font-black uppercase tracking-wider transition-all border ${isAdmin ? 'bg-emerald-500 border-emerald-400 text-white shadow-xl scale-105' : 'bg-white/10 border-white/20 text-white hover:bg-white/20'}`}>
                {isAdmin ? <Lock className="w-5 h-5" /> : <ShieldCheck className="w-5 h-5" />}
                {isAdmin ? 'Mod Pentadbir' : 'Pentadbir'}
              </button>
            </div>
            <div className="text-xs font-bold text-blue-100 flex items-center gap-2 bg-white/5 px-4 py-2 rounded-xl">
              <Calendar className="w-4 h-4 text-amber-400" />
              {new Date().toLocaleDateString('ms-MY', { weekday: 'long', day: 'numeric', month: 'long', year: 'numeric' })}
            </div>
          </div>
        </div>
      </header>

      {/* Bar Statistik */}
      <div className="max-w-7xl mx-auto px-4 -mt-10 grid grid-cols-2 md:grid-cols-4 gap-4 relative z-20">
        {Object.entries(stats).map(([key, stat]) => (
          <button 
            key={key} 
            onClick={() => setStatDetailModal({ title: stat.label, list: stat.list })} 
            className="bg-white p-6 rounded-[1.5rem] shadow-xl border border-slate-100 flex flex-col text-left hover:border-blue-400 hover:-translate-y-1 transition-all active:scale-95 group"
          >
            <span className="text-[10px] uppercase tracking-widest font-black text-slate-400 mb-2 group-hover:text-blue-500 transition-colors">{stat.label}</span>
            <div className="flex items-center justify-between">
              <span className="text-3xl font-black text-slate-700">{stat.value}</span>
              <Users className="w-6 h-6 text-slate-200 group-hover:text-blue-200 transition-colors" />
            </div>
          </button>
        ))}
      </div>

      <div className="max-w-7xl mx-auto px-4 mt-12">
        {/* Minggu Navigation & Pie Chart */}
        <div className="bg-white p-6 md:p-8 rounded-[3rem] shadow-sm border border-slate-100 mb-10 flex flex-col md:flex-row items-center gap-10">
          <div className="flex items-center gap-6 bg-slate-50 p-3 rounded-[2rem] border border-slate-200">
            <button onClick={() => setCurrentWeekIdx(Math.max(0, currentWeekIdx - 1))} className="p-4 hover:bg-white hover:shadow-md rounded-2xl transition-all text-slate-400 hover:text-[#1e3a5f]"><ChevronLeft className="w-8 h-8"/></button>
            <div className="text-center min-w-[160px] px-4">
              <h2 className="text-3xl font-black text-[#1e3a5f] tracking-tighter leading-none">{currentWeek.label}</h2>
              <p className="text-[10px] font-black text-blue-500 mt-2 uppercase tracking-[0.2em] flex items-center justify-center gap-2">
                <Calendar className="w-3 h-3" />
                {currentWeek.monday.toLocaleDateString('ms-MY', { day: 'numeric', month: 'short' })} — {currentWeek.friday.toLocaleDateString('ms-MY', { day: 'numeric', month: 'short', year: 'numeric' })}
              </p>
            </div>
            <button onClick={() => setCurrentWeekIdx(Math.min(51, currentWeekIdx + 1))} className="p-4 hover:bg-white hover:shadow-md rounded-2xl transition-all text-slate-400 hover:text-[#1e3a5f]"><ChevronRight className="w-8 h-8"/></button>
          </div>

          <div className="flex items-center gap-8 bg-slate-50 p-5 rounded-[2.5rem] border border-slate-200 flex-1 w-full md:w-auto">
            <SimplePieChart verified={stats.verified.value} unsubmitted={stats.unsubmitted.value} late={stats.late.value} total={stats.total.value} />
            <div className="grid grid-cols-1 gap-2 flex-1">
              <div className="flex items-center justify-between"><div className="flex items-center gap-3"><div className="w-3 h-3 rounded-full bg-emerald-500" /><span className="text-[10px] font-black text-slate-500 uppercase">Siap Disahkan</span></div><span className="text-xs font-black text-slate-800">{stats.verified.value}</span></div>
              <div className="flex items-center justify-between"><div className="flex items-center gap-3"><div className="w-3 h-3 rounded-full bg-amber-500" /><span className="text-[10px] font-black text-slate-500 uppercase">Belum Hantar</span></div><span className="text-xs font-black text-slate-800">{stats.unsubmitted.value}</span></div>
              <div className="flex items-center justify-between"><div className="flex items-center gap-3"><div className="w-3 h-3 rounded-full bg-rose-500" /><span className="text-[10px] font-black text-slate-500 uppercase">Penghantaran Lewat</span></div><span className="text-xs font-black text-slate-800">{stats.late.value}</span></div>
            </div>
          </div>
        </div>

        {/* Tab Penapis */}
        <div className="flex gap-3 overflow-x-auto pb-6 mb-8 border-b border-slate-100">
          {Object.entries(CATEGORIES).map(([key, cat]) => (
            <button key={key} onClick={() => setActiveTab(key)} className={`px-6 py-3 rounded-2xl text-xs font-black uppercase tracking-widest transition-all ${activeTab === key ? 'bg-[#1e3a5f] text-white shadow-xl' : 'bg-white text-slate-500 border border-slate-200 hover:border-[#1e3a5f]'}`}>{cat.label}</button>
          ))}
        </div>

        {/* Senarai Staf */}
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
          {filteredStaff.map(staff => {
            const sub = submissions.find(s => s.staff_id === staff.id && s.week_key === currentWeek.key);
            let sLabel = 'Belum Hantar';
            let sColorClass = 'bg-slate-50 text-slate-600';
            if (sub) {
              if (sub.status === 'verified') { sLabel = 'Disahkan'; sColorClass = 'bg-emerald-50 text-emerald-600'; }
              else if (sub.is_late) { sLabel = 'Lewat'; sColorClass = 'bg-rose-50 text-rose-600'; }
              else { sLabel = 'Dihantar'; sColorClass = 'bg-amber-50 text-amber-600'; }
            }
            const initials = getInitials(staff.name);
            const cardStyle = CATEGORY_STYLES[staff.category] || '';

            return (
              <div key={staff.id} onClick={() => setSelectedStaff(staff)} className="group bg-white rounded-[2rem] p-6 border border-slate-100 shadow-sm hover:shadow-2xl hover:-translate-y-2 transition-all duration-300 cursor-pointer">
                <div className="flex items-start justify-between mb-6">
                  <div className={`w-14 h-14 rounded-2xl flex items-center justify-center font-black text-lg border transition-transform group-hover:rotate-6 ${cardStyle}`}>{initials}</div>
                  <div className={`px-3 py-1.5 rounded-xl text-[9px] font-black uppercase tracking-tighter ${sColorClass}`}>{sLabel}</div>
                </div>
                <h3 className="font-black text-slate-800 text-sm line-clamp-1 group-hover:text-blue-700 transition-colors uppercase tracking-tight">{staff.name}</h3>
                <p className="text-[10px] font-bold text-slate-400 mt-1 mb-6 uppercase tracking-widest">{staff.role}</p>
                {sub && (
                  <div className="flex items-center justify-between pt-5 border-t border-slate-50">
                    <span className="text-[10px] font-black text-slate-400 flex items-center gap-2"><FileText className="w-4 h-4 text-blue-400" /> {sub.file_name.substring(0, 10)}...</span>
                    <div className="bg-blue-50 text-blue-600 p-2 rounded-xl group-hover:bg-blue-600 group-hover:text-white transition-all"><Eye className="w-4 h-4" /></div>
                  </div>
                )}
              </div>
            );
          })}
        </div>
      </div>

      {/* MODAL NOTIFIKASI */}
      {showNotifPanel && (
        <div className="fixed inset-0 z-[500] flex items-center justify-center p-4 bg-slate-900/80 backdrop-blur-md">
          <div className="bg-white rounded-[3rem] w-full max-w-lg shadow-2xl overflow-hidden flex flex-col border-4 border-blue-400/20">
            <div className="p-8 bg-gradient-to-r from-[#1e3a5f] to-[#0c2340] text-white flex justify-between items-center shadow-lg">
              <div className="flex items-center gap-4">
                <div className="p-3 bg-white/20 rounded-2xl"><BellRing className="w-6 h-6 text-amber-400" /></div>
                <div>
                  <h3 className="text-lg font-black uppercase tracking-widest leading-none">Pusat Notifikasi</h3>
                  <p className="text-[10px] text-blue-300 font-bold mt-1 uppercase tracking-tighter">Aktiviti Terkini</p>
                </div>
              </div>
              <button onClick={() => setShowNotifPanel(false)} className="p-3 bg-white/10 hover:bg-white/20 rounded-2xl transition-all border border-white/10"><X className="w-6 h-6 text-white"/></button>
            </div>
            
            <div className="flex-1 overflow-y-auto max-h-[60vh] p-4 space-y-3 bg-slate-50">
              {notifications.length === 0 ? (
                <div className="p-16 text-center">
                  <History className="w-16 h-16 text-slate-200 mx-auto mb-4" />
                  <p className="text-sm text-slate-400 font-black uppercase tracking-widest">Tiada Aktiviti</p>
                </div>
              ) : (
                notifications.map(n => (
                  <div key={n.id} className="bg-white p-6 rounded-[2rem] border border-slate-200 shadow-sm flex gap-5 items-start transition-all">
                    <div className={`w-3 h-3 rounded-full mt-2 flex-shrink-0 animate-pulse ${n.type === 'success' ? 'bg-emerald-500' : n.type === 'warning' ? 'bg-rose-500' : 'bg-blue-500'}`} />
                    <div className="flex-1">
                      <p className="text-[10px] font-black text-blue-600 uppercase tracking-widest mb-1">{n.title}</p>
                      <p className="text-sm text-slate-800 font-black leading-relaxed">{n.message}</p>
                      <div className="flex items-center gap-2 mt-4 pt-4 border-t border-slate-100">
                        <Clock className="w-3 h-3 text-slate-300" />
                        <p className="text-[10px] text-slate-400 font-bold italic">{new Date(n.timestamp).toLocaleString('ms-MY')}</p>
                      </div>
                    </div>
                  </div>
                ))
              )}
            </div>
            <div className="p-6 bg-white border-t border-slate-100"><button onClick={() => setShowNotifPanel(false)} className="w-full bg-[#1e3a5f] text-white font-black py-4 rounded-2xl uppercase text-xs tracking-[0.3em]">Tutup</button></div>
          </div>
        </div>
      )}

      {/* Modal: Passcode */}
      {showPasscodeModal && (
        <div className="fixed inset-0 z-[600] flex items-center justify-center p-4 bg-slate-900/80 backdrop-blur-xl">
          <div className="bg-white rounded-[3rem] w-full max-sm shadow-2xl p-10 text-center">
            <div className="w-20 h-20 bg-blue-50 rounded-3xl flex items-center justify-center mx-auto mb-6"><KeyRound className="w-10 h-10 text-blue-600" /></div>
            <h2 className="text-xl font-black text-[#1e3a5f] uppercase tracking-widest">Akses Pentadbir</h2>
            <input type="password" maxLength={4} value={passcodeInput} onChange={(e) => setPasscodeInput(e.target.value)} onKeyDown={(e) => e.key === 'Enter' && submitPasscode()} autoFocus className="w-full mt-8 bg-slate-50 border-4 border-slate-100 rounded-[2rem] py-6 text-center text-4xl font-black tracking-[1.5rem] outline-none focus:border-blue-400 text-[#1e3a5f]" placeholder="****" />
            <div className="grid grid-cols-2 gap-4 mt-10">
              <button onClick={() => setShowPasscodeModal(false)} className="bg-slate-100 text-slate-500 font-black py-4 rounded-2xl text-xs uppercase tracking-widest">Batal</button>
              <button onClick={submitPasscode} className="bg-[#1e3a5f] text-white font-black py-4 rounded-2xl text-xs uppercase tracking-widest">Masuk</button>
            </div>
          </div>
        </div>
      )}

      {/* Modal: Detail / Upload */}
      {selectedStaff && (
        <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm">
          <div className="bg-white rounded-[3rem] w-full max-w-xl shadow-2xl overflow-hidden">
            <div className="p-8 border-b border-slate-100 flex justify-between items-start bg-slate-50/50">
              <div>
                <h2 className="text-2xl font-black text-[#1e3a5f] uppercase tracking-tighter">{selectedStaff.name}</h2>
                <p className="text-[11px] font-black text-blue-500 mt-2 uppercase tracking-[0.3em]">{currentWeek.label} • {selectedStaff.role}</p>
              </div>
              <button onClick={() => setSelectedStaff(null)} className="p-3 bg-white shadow-sm border border-slate-200 rounded-full"><X className="w-6 h-6 text-slate-400" /></button>
            </div>
            <div className="p-8">
              {(() => {
                const sub = submissions.find(s => s.staff_id === selectedStaff.id && s.week_key === currentWeek.key);
                if (sub) {
                  return (
                    <div className="space-y-8">
                      <div className={`p-6 rounded-[2rem] border flex items-center gap-6 ${sub.is_late ? 'bg-rose-50 border-rose-100' : 'bg-blue-50 border-blue-100'}`}>
                        <div className={`p-4 rounded-2xl text-white ${sub.is_late ? 'bg-rose-600' : 'bg-blue-600'}`}><FileText className="w-8 h-8" /></div>
                        <div className="flex-1">
                          <p className={`text-base font-black uppercase ${sub.is_late ? 'text-rose-900' : 'text-blue-900'}`}>{sub.file_name}</p>
                          <p className="text-[10px] font-black uppercase mt-1 tracking-widest text-slate-400">Dihantar: {new Date(sub.submitted_at).toLocaleString('ms-MY')}</p>
                        </div>
                        <button onClick={() => setViewingFile(sub)} className="p-4 bg-white rounded-2xl shadow-sm border border-slate-200 hover:scale-110 transition-transform"><Eye className="w-8 h-8 text-blue-600"/></button>
                      </div>
                      
                      {sub.status === 'verified' ? (
                        <div className="bg-emerald-50 p-6 rounded-[2rem] border border-emerald-100 flex items-start gap-6">
                          <CheckCircle className="text-emerald-500 w-10 h-10" />
                          <div><p className="text-sm font-black text-emerald-900 uppercase">Tugasan Disahkan</p>{sub.notes && <p className="mt-4 p-4 bg-white/60 rounded-2xl text-xs italic text-slate-700">"{sub.notes}"</p>}</div>
                        </div>
                      ) : isAdmin ? (
                        <div className="space-y-6 pt-8 border-t border-slate-100">
                          <textarea value={verifyNotes} onChange={(e) => setVerifyNotes(e.target.value)} className="w-full bg-slate-50 border-4 border-slate-100 rounded-[2rem] p-6 text-sm h-40 outline-none focus:border-blue-200" placeholder="Tulis catatan pengetua..." />
                          <div className="grid grid-cols-2 gap-4">
                            <button onClick={() => verifyTask(sub)} disabled={isProcessing} className="bg-emerald-600 text-white font-black py-5 rounded-2xl transition-all flex items-center justify-center gap-3 uppercase text-xs tracking-widest">
                              {isProcessing ? <RefreshCw className="w-5 h-5 animate-spin" /> : <UserCheck className="w-5 h-5"/>} Sahkan
                            </button>
                            <button onClick={() => deleteTask(sub.id)} className="bg-rose-50 text-rose-600 font-black py-5 rounded-2xl flex items-center justify-center gap-3 uppercase text-xs tracking-widest"><Trash2 className="w-5 h-5"/> Padam</button>
                          </div>
                        </div>
                      ) : <div className="text-center py-16 bg-slate-50/30 rounded-[3rem] border-4 border-dashed border-slate-100"><Clock className="w-16 h-16 text-amber-500 mx-auto mb-4 animate-pulse" /><p className="text-xl font-black text-[#1e3a5f] uppercase tracking-widest">Menunggu Pengesahan</p></div>}
                    </div>
                  );
                }
                return (
                  <div className="space-y-8">
                    <div onClick={() => document.getElementById('f-up').click()} className="border-4 border-dashed border-slate-200 rounded-[3rem] p-16 text-center hover:bg-blue-50/50 hover:border-blue-300 transition-all cursor-pointer bg-slate-50/30">
                      <input id="f-up" type="file" hidden onChange={handleFileChange} />
                      {uploadData.base64 ? (
                        <div className="flex flex-col items-center">
                          <CheckCircle className="w-20 h-20 text-emerald-500 mb-4 animate-bounce" />
                          <p className="text-lg font-black text-slate-800 uppercase">{uploadData.file.name}</p>
                        </div>
                      ) : (
                        <>
                          <div className="bg-white w-24 h-24 rounded-[2rem] shadow-sm flex items-center justify-center mx-auto mb-6"><UploadCloud className="w-12 h-12 text-blue-500" /></div>
                          <p className="text-lg font-black text-slate-800 uppercase tracking-widest">Muat Naik Fail</p>
                          <p className="text-xs font-bold text-slate-400 mt-2">Maksimum 1MB</p>
                        </>
                      )}
                    </div>
                    <button disabled={!uploadData.base64 || isProcessing} onClick={submitTask} className="w-full bg-[#1e3a5f] text-white font-black py-6 rounded-[2rem] shadow-2xl disabled:opacity-50 transition-all uppercase tracking-[0.2em]">
                      {isProcessing ? <RefreshCw className="w-6 h-6 animate-spin" /> : <FileText className="w-6 h-6" />} Simpan Fail
                    </button>
                  </div>
                );
              })()}
            </div>
          </div>
        </div>
      )}

      {/* Imej Viewer */}
      {viewingFile && (
        <div className="fixed inset-0 z-[700] flex items-center justify-center p-4 bg-slate-900/98 backdrop-blur-3xl">
          <div className="w-full max-w-5xl bg-white rounded-[3rem] overflow-hidden shadow-2xl">
            <div className="p-8 flex justify-between items-center border-b border-slate-100">
              <span className="text-sm font-black text-[#1e3a5f] uppercase">{viewingFile.file_name}</span>
              <div className="flex gap-2">
                <a href={viewingFile.file_data} download={viewingFile.file_name} className="p-4 bg-emerald-50 text-emerald-600 rounded-2xl flex items-center gap-2 font-black text-xs uppercase"><Download className="w-5 h-5" /> Muat Turun</a>
                <button onClick={() => setViewingFile(null)} className="p-4 bg-slate-50 rounded-2xl"><X className="w-8 h-8 text-slate-500" /></button>
              </div>
            </div>
            <div className="p-6 md:p-12 bg-slate-100 flex justify-center items-center overflow-auto max-h-[85vh]">
              {viewingFile.file_type?.startsWith('image/') ? <img src={viewingFile.file_data} alt="Paparan" className="max-w-full rounded-[2rem] shadow-2xl border-8 border-white" /> : (
                <div className="p-20 text-center bg-white rounded-[3rem] shadow-xl border border-slate-200">
                  <FileText className="w-24 h-24 text-blue-500 mx-auto mb-6" />
                  <p className="text-xl font-black text-[#1e3a5f] uppercase">Fail Berjaya Dibuka</p>
                  <p className="text-xs text-slate-500 mt-6 max-w-xs">Sila klik butang Muat Turun untuk melihat kandungan fail bukan imej.</p>
                </div>
              )}
            </div>
          </div>
        </div>
      )}

      {/* Toast */}
      {toast && (
        <div className={`fixed bottom-12 left-1/2 -translate-x-1/2 z-[1000] px-10 py-5 rounded-[2rem] shadow-2xl flex items-center gap-4 text-white border-4 border-white/20 ${toast.type === 'success' ? 'bg-emerald-600' : toast.type === 'error' ? 'bg-rose-600' : 'bg-[#1e3a5f]'}`}>
          {toast.type === 'success' ? <CheckCircle className="w-8 h-8"/> : <Info className="w-8 h-8"/>}
          <span className="text-base font-black tracking-widest uppercase">{toast.message}</span>
        </div>
      )}

      {/* Modal Detail Statistik */}
      {statDetailModal && (
        <div className="fixed inset-0 z-[650] flex items-center justify-center p-4 bg-slate-900/70 backdrop-blur-md">
          <div className="bg-white rounded-[3rem] w-full max-w-lg shadow-2xl overflow-hidden">
            <div className="p-8 border-b border-slate-100 flex justify-between items-center">
              <div><h3 className="text-xl font-black text-[#1e3a5f] uppercase">{statDetailModal.title}</h3><p className="text-xs text-slate-400 font-bold uppercase mt-1">Minggu Ini</p></div>
              <button onClick={() => setStatDetailModal(null)} className="p-3 bg-slate-50 rounded-2xl"><X className="w-6 h-6 text-slate-500" /></button>
            </div>
            <div className="p-6 max-h-[60vh] overflow-y-auto space-y-3 bg-slate-50">
              {statDetailModal.list.length === 0 ? <div className="bg-white p-8 text-center rounded-[2rem]"><p className="text-sm font-black text-slate-500">Tiada rekod.</p></div> : 
                statDetailModal.list.map(s => <div key={s.id} className="bg-white p-5 rounded-[1.5rem] border border-slate-200"><p className="text-sm font-black text-slate-800 uppercase">{s.name}</p><p className="text-[10px] text-slate-400 font-bold uppercase">{s.role}</p></div>)
              }
            </div>
          </div>
        </div>
      )}
    </div>
  );
}


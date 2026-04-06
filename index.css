/**
 * @license
 * SPDX-License-Identifier: Apache-2.0
 */

import React, { useState, useEffect, useMemo } from 'react';
import { 
  Plus, 
  Trash2, 
  RotateCcw, 
  Download, 
  TrendingUp, 
  TrendingDown, 
  Award, 
  Lock, 
  Unlock,
  ChevronRight,
  ChevronDown,
  Settings2,
  History,
  AlertCircle,
  Save,
  BookOpen,
  Sparkles,
  Zap,
  Moon,
  Sun,
  Palette,
  X,
  Star,
  Heart
} from 'lucide-react';
import { motion, AnimatePresence } from 'motion/react';

// Types
type SubjectType = 'Talento' | 'Sforzo' | 'Standard';
type Semester = 'Q1' | 'Q2';
type Theme = 'indigo' | 'emerald' | 'rose' | 'amber' | 'violet';

interface Grade {
  id: string;
  value: number;
  label: string; // e.g. "8+", "7-"
  timestamp: number;
}

interface SubjectData {
  name: string;
  type: SubjectType;
  grades: {
    Q1: Grade[];
    Q2: Grade[];
  };
}

const PREDEFINED_SUBJECTS = [
  'Scienze', 'Italiano', 'Matematica', 'Arte', 'Storia', 'Spagnolo', 
  'Geografia', 'Inglese', 'Educazione Civica', 'Musica', 'Tecnologia', 'Educazione Fisica'
];

const GRADE_MAP: Record<string, number> = {
  '10': 10, '9.5': 9.5, '9': 9, '8.5': 8.5, '8': 8, '7.5': 7.5, '7': 7, '6.5': 6.5, '6': 6, '5.5': 5.5, '5': 5, '4.5': 4.5, '4': 4, '3.5': 3.5, '3': 3,
  '10-': 9.75, '9+': 9.25, '9-': 8.75, '8+': 8.25, '8-': 7.75, '7+': 7.25, '7-': 6.75, '6+': 6.25, '6-': 5.75, '5+': 5.25, '5-': 4.75, '4+': 4.25, '4-': 3.75, '3+': 3.25, '3-': 2.75
};

const formatDate = (timestamp: number) => {
  return new Date(timestamp).toLocaleDateString('it-IT', {
    day: '2-digit',
    month: '2-digit',
    year: 'numeric'
  });
};

const THEME_CONFIG: Record<Theme, { 
  primary: string, 
  secondary: string, 
  accent: string, 
  gradient: string, 
  glow: string,
  // Full class names for reliable generation
  textPrimary: string,
  textAccent: string,
  bgPrimary: string,
  bgSecondary: string,
  bgSecondary50: string,
  borderPrimary: string,
  borderSecondary: string,
  borderSecondary50: string,
  shadowGlow: string,
  shadowPrimary20: string,
  fromPrimary: string,
  toAccent: string,
  toSecondary30: string,
  // Dark mode specific theme accents
  bgPrimaryDark: string,
  textPrimaryDark: string,
  bgPrimarySolidDark: string,
  shadowPrimaryDark: string,
}> = {
  indigo: { 
    primary: 'indigo-500', secondary: 'indigo-50', accent: 'indigo-600', 
    gradient: 'from-indigo-50/50 via-white to-purple-50/50', 
    glow: 'indigo-500/30',
    textPrimary: 'text-indigo-700',
    textAccent: 'text-indigo-900',
    bgPrimary: 'bg-indigo-500',
    bgSecondary: 'bg-indigo-50',
    bgSecondary50: 'bg-indigo-50/50',
    borderPrimary: 'border-indigo-500',
    borderSecondary: 'border-indigo-50',
    borderSecondary50: 'border-indigo-50/50',
    shadowGlow: 'shadow-indigo-500/30',
    shadowPrimary20: 'shadow-indigo-500/20',
    fromPrimary: 'from-indigo-500',
    toAccent: 'to-indigo-600',
    toSecondary30: 'to-indigo-50/30',
    bgPrimaryDark: 'bg-indigo-900/30',
    textPrimaryDark: 'text-indigo-400',
    bgPrimarySolidDark: 'bg-indigo-600',
    shadowPrimaryDark: 'shadow-indigo-900/20',
  },
  emerald: { 
    primary: 'emerald-500', secondary: 'emerald-50', accent: 'emerald-600', 
    gradient: 'from-emerald-50/50 via-white to-teal-50/50', 
    glow: 'emerald-500/30',
    textPrimary: 'text-emerald-700',
    textAccent: 'text-emerald-900',
    bgPrimary: 'bg-emerald-500',
    bgSecondary: 'bg-emerald-50',
    bgSecondary50: 'bg-emerald-50/50',
    borderPrimary: 'border-emerald-500',
    borderSecondary: 'border-emerald-50',
    borderSecondary50: 'border-emerald-50/50',
    shadowGlow: 'shadow-emerald-500/30',
    shadowPrimary20: 'shadow-emerald-500/20',
    fromPrimary: 'from-emerald-500',
    toAccent: 'to-emerald-600',
    toSecondary30: 'to-emerald-50/30',
    bgPrimaryDark: 'bg-emerald-900/30',
    textPrimaryDark: 'text-emerald-400',
    bgPrimarySolidDark: 'bg-emerald-600',
    shadowPrimaryDark: 'shadow-emerald-900/20',
  },
  rose: { 
    primary: 'rose-500', secondary: 'rose-50', accent: 'rose-600', 
    gradient: 'from-rose-50/50 via-white to-pink-50/50', 
    glow: 'rose-500/30',
    textPrimary: 'text-rose-700',
    textAccent: 'text-rose-900',
    bgPrimary: 'bg-rose-500',
    bgSecondary: 'bg-rose-50',
    bgSecondary50: 'bg-rose-50/50',
    borderPrimary: 'border-rose-500',
    borderSecondary: 'border-rose-50',
    borderSecondary50: 'border-rose-50/50',
    shadowGlow: 'shadow-rose-500/30',
    shadowPrimary20: 'shadow-rose-500/20',
    fromPrimary: 'from-rose-500',
    toAccent: 'to-rose-600',
    toSecondary30: 'to-rose-50/30',
    bgPrimaryDark: 'bg-rose-900/30',
    textPrimaryDark: 'text-rose-400',
    bgPrimarySolidDark: 'bg-rose-600',
    shadowPrimaryDark: 'shadow-rose-900/20',
  },
  amber: { 
    primary: 'amber-500', secondary: 'amber-50', accent: 'amber-600', 
    gradient: 'from-amber-50/50 via-white to-orange-50/50', 
    glow: 'amber-500/30',
    textPrimary: 'text-amber-700',
    textAccent: 'text-amber-900',
    bgPrimary: 'bg-amber-500',
    bgSecondary: 'bg-amber-50',
    bgSecondary50: 'bg-amber-50/50',
    borderPrimary: 'border-amber-500',
    borderSecondary: 'border-amber-50',
    borderSecondary50: 'border-amber-50/50',
    shadowGlow: 'shadow-amber-500/30',
    shadowPrimary20: 'shadow-amber-500/20',
    fromPrimary: 'from-amber-500',
    toAccent: 'to-amber-600',
    toSecondary30: 'to-amber-50/30',
    bgPrimaryDark: 'bg-amber-900/30',
    textPrimaryDark: 'text-amber-400',
    bgPrimarySolidDark: 'bg-amber-600',
    shadowPrimaryDark: 'shadow-amber-900/20',
  },
  violet: { 
    primary: 'violet-500', secondary: 'violet-50', accent: 'violet-600', 
    gradient: 'from-violet-50/50 via-white to-purple-50/50', 
    glow: 'violet-500/30',
    textPrimary: 'text-violet-700',
    textAccent: 'text-violet-900',
    bgPrimary: 'bg-violet-500',
    bgSecondary: 'bg-violet-50',
    bgSecondary50: 'bg-violet-50/50',
    borderPrimary: 'border-violet-500',
    borderSecondary: 'border-violet-50',
    borderSecondary50: 'border-violet-50/50',
    shadowGlow: 'shadow-violet-500/30',
    shadowPrimary20: 'shadow-violet-500/20',
    fromPrimary: 'from-violet-500',
    toAccent: 'to-violet-600',
    toSecondary30: 'to-violet-50/30',
    bgPrimaryDark: 'bg-violet-900/30',
    textPrimaryDark: 'text-violet-400',
    bgPrimarySolidDark: 'bg-violet-600',
    shadowPrimaryDark: 'shadow-violet-900/20',
  },
};

// Sparkle Component for grade buttons
const SparkleEffect = ({ trigger, intensity, isDarkMode }: { trigger: number, intensity: number, isDarkMode: boolean }) => {
  const [sparks, setSparks] = React.useState<{ id: number; x: number; y: number; s: number; d: number; c: string }[]>([]);

  React.useEffect(() => {
    if (trigger > 0) {
      const count = Math.floor(5 + intensity * 5);
      const colors = intensity > 0.7 ? ['#FBBF24', '#F59E0B', '#FFFFFF'] : ['#34D399', '#60A5FA', '#FFFFFF'];
      const newSparks = Array.from({ length: count }).map((_, i) => ({
        id: Math.random(),
        x: (Math.random() - 0.5) * (50 + intensity * 30),
        y: -Math.random() * (40 + intensity * 40) - 15,
        s: Math.random() * 0.6 + 0.4,
        d: Math.random() * 0.15,
        c: colors[Math.floor(Math.random() * colors.length)]
      }));
      setSparks(prev => [...prev, ...newSparks]);
      setTimeout(() => {
        setSparks(prev => prev.filter(s => !newSparks.includes(s)));
      }, 800);
    }
  }, [trigger, intensity]);

  return (
    <div className="absolute inset-0 pointer-events-none overflow-visible z-30">
      <AnimatePresence>
        {sparks.map((spark) => (
          <motion.div
            key={spark.id}
            initial={{ x: 0, y: 0, scale: 0, opacity: 1, rotate: 0 }}
            animate={{ 
              x: spark.x, 
              y: spark.y, 
              scale: [0, spark.s * 1.5, 0], 
              opacity: [1, 1, 0],
              rotate: 180 
            }}
            transition={{ duration: 0.6, ease: "easeOut", delay: spark.d }}
            className="absolute left-1/2 top-0 -translate-x-1/2"
            style={{ color: spark.c }}
          >
            <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" className="drop-shadow-[0_0_5px_currentColor]">
              <path d="M12 0L14.59 9.41L24 12L14.59 14.59L12 24L9.41 14.59L0 12L9.41 9.41L12 0Z" />
            </svg>
          </motion.div>
        ))}
      </AnimatePresence>
    </div>
  );
};

// GradeButton Component for internal animations
const GradeButton = ({ label, val, colorClass, hoverScale, isDarkMode, onClick }: any) => {
  const [trigger, setTrigger] = React.useState(0);
  const intensity = (val - 6) / 4;

  return (
    <motion.button
      whileHover={{ scale: hoverScale, y: val >= 6 ? -5 : 0 }}
      whileTap={{ scale: 0.95 }}
      onClick={() => {
        if (val >= 6) setTrigger(prev => prev + 1);
        onClick();
      }}
      className={`relative py-2.5 md:py-3 rounded-xl text-xs font-black transition-all shadow-sm ${colorClass} ${val >= 9 && !isDarkMode ? 'ring-2 ring-emerald-200' : ''} ${val >= 9 && isDarkMode ? 'ring-2 ring-emerald-900/50' : ''}`}
    >
      {val >= 6 && <SparkleEffect trigger={trigger} intensity={intensity} isDarkMode={isDarkMode} />}
      <span className="relative z-10">{label}</span>
    </motion.button>
  );
};

export default function App() {
  // State
  const [subjects, setSubjects] = useState<SubjectData[]>([]);
  const [isConfigured, setIsConfigured] = useState(false);
  const [lastSelectedSubject, setLastSelectedSubject] = useState<string>('');
  const [lastSelectedSemester, setLastSelectedSemester] = useState<Semester>('Q1');
  const [showResetConfirm, setShowResetConfirm] = useState(false);
  const [isSubjectDropdownOpen, setIsSubjectDropdownOpen] = useState(false);
  const [isSettingsOpen, setIsSettingsOpen] = useState(false);
  const [theme, setTheme] = useState<Theme>('indigo');
  const [isDarkMode, setIsDarkMode] = useState(false);

  // Initialization
  useEffect(() => {
    const savedData = localStorage.getItem('grade_rewards_data');
    if (savedData) {
      const parsed = JSON.parse(savedData);
      setSubjects(parsed.subjects);
      setIsConfigured(parsed.isConfigured);
      if (parsed.theme) setTheme(parsed.theme);
      if (parsed.isDarkMode !== undefined) setIsDarkMode(parsed.isDarkMode);
    } else {
      setSubjects(PREDEFINED_SUBJECTS.map(name => ({
        name,
        type: 'Standard',
        grades: { Q1: [], Q2: [] }
      })));
    }
  }, []);

  // Persistence
  useEffect(() => {
    if (subjects.length > 0) {
      localStorage.setItem('grade_rewards_data', JSON.stringify({ 
        subjects, 
        isConfigured, 
        theme, 
        isDarkMode 
      }));
    }
  }, [subjects, isConfigured, theme, isDarkMode]);

  // Calculations
  const calculateReward = (grade: number, semester: Semester, type: SubjectType): number => {
    if (semester === 'Q1') {
      if (grade >= 9.5) return 10;
      if (grade >= 8) return 8;
      if (grade >= 6) return 5;
      return -5;
    } else {
      if (type === 'Talento') {
        if (grade >= 9) return 10;
        if (grade >= 8) return 5;
        if (grade >= 6.5) return 0;
        if (grade >= 6) return -5;
        return -10;
      } else if (type === 'Sforzo') {
        if (grade >= 9) return 20;
        if (grade >= 8) return 15;
        if (grade >= 7) return 10;
        if (grade >= 6) return 5;
        return -5;
      } else {
        if (grade >= 9) return 10;
        if (grade >= 8) return 5;
        if (grade >= 7) return 2;
        if (grade >= 6) return 0;
        return -5;
      }
    }
  };

  const calculateRecoveryBonuses = (grades: Grade[]): number => {
    let bonuses = 0;
    for (let i = 1; i < grades.length; i++) {
      if (grades[i-1].value < 6 && grades[i].value >= 6) {
        bonuses += 15;
      }
    }
    return bonuses;
  };

  const stats = useMemo(() => {
    let totalBalance = 0;
    let isFrozen = false;
    
    let allQ1Grades: number[] = [];
    let allQ2Grades: number[] = [];

    const subjectStats = subjects.map(s => {
      const q1Rewards = s.grades.Q1.reduce((acc, g) => acc + calculateReward(g.value, 'Q1', s.type), 0);
      const q2Rewards = s.grades.Q2.reduce((acc, g) => acc + calculateReward(g.value, 'Q2', s.type), 0);
      
      const q1Recovery = calculateRecoveryBonuses(s.grades.Q1);
      const q2Recovery = calculateRecoveryBonuses(s.grades.Q2);
      
      const totalSubjectReward = q1Rewards + q2Rewards + q1Recovery + q2Recovery;
      totalBalance += totalSubjectReward;

      const lastQ2Grade = s.grades.Q2.length > 0 ? s.grades.Q2[s.grades.Q2.length - 1].value : null;
      if (lastQ2Grade !== null && lastQ2Grade < 6) {
        isFrozen = true;
      }

      const q1Values = s.grades.Q1.map(g => g.value);
      const q2Values = s.grades.Q2.map(g => g.value);
      
      allQ1Grades.push(...q1Values);
      allQ2Grades.push(...q2Values);

      const q1Avg = q1Values.length > 0 ? q1Values.reduce((a, b) => a + b, 0) / q1Values.length : 0;
      const q2Avg = q2Values.length > 0 ? q2Values.reduce((a, b) => a + b, 0) / q2Values.length : 0;
      const totalAvg = [...q1Values, ...q2Values].length > 0 ? [...q1Values, ...q2Values].reduce((a, b) => a + b, 0) / [...q1Values, ...q2Values].length : 0;

      const subjectImprovementBonus = (q1Avg > 0 && q2Avg > q1Avg) ? 15 : 0;

      return {
        ...s,
        q1Avg,
        q2Avg,
        avg: totalAvg,
        totalReward: totalSubjectReward,
        recoveryBonuses: q1Recovery + q2Recovery,
        improvementBonus: subjectImprovementBonus,
        lastQ2Grade
      };
    });

    const overallAvgQ1 = allQ1Grades.length > 0 ? allQ1Grades.reduce((a, b) => a + b, 0) / allQ1Grades.length : 0;
    const overallAvgQ2 = allQ2Grades.length > 0 ? allQ2Grades.reduce((a, b) => a + b, 0) / allQ2Grades.length : 0;
    
    const allGrades = [...allQ1Grades, ...allQ2Grades];
    const overallAvgTotal = allGrades.length > 0 ? allGrades.reduce((a, b) => a + b, 0) / allGrades.length : 0;

    const totalPotentialBonus = subjectStats.reduce((acc, s) => acc + s.improvementBonus, 0);

    return { 
      totalBalance, 
      isFrozen, 
      subjectStats, 
      overallAvgQ1, 
      overallAvgQ2, 
      overallAvgTotal,
      improvementBonus: totalPotentialBonus 
    };
  }, [subjects]);

  // Handlers
  const handleTypeChange = (name: string, type: SubjectType) => {
    setSubjects(prev => prev.map(s => s.name === name ? { ...s, type } : s));
  };

  const currentTheme = THEME_CONFIG[theme];

  // Render Configuration View
  if (!isConfigured) {
    return (
      <div className={`min-h-screen p-3 md:p-8 font-sans transition-all duration-700 ${isDarkMode ? 'bg-slate-950 text-slate-300' : `bg-gradient-to-br ${currentTheme.gradient} text-slate-900`}`}>
        <div className="max-w-5xl mx-auto">
          <header className={`flex flex-col md:flex-row justify-between items-center mb-4 md:mb-10 p-5 md:p-8 rounded-[1.5rem] md:rounded-[2rem] shadow-xl border-2 transition-all gap-4 md:gap-6 ${isDarkMode ? 'bg-slate-900 border-slate-800 shadow-black/20' : `bg-white ${currentTheme.borderSecondary50} ${currentTheme.shadowGlow}`}`}>
            <div className="text-center md:text-left">
              <h1 className={`text-2xl md:text-4xl font-black tracking-tight mb-1 ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>Ehi! Configuriamo? 🎨</h1>
              <p className={`text-sm md:text-lg font-medium ${isDarkMode ? 'text-slate-500' : `${currentTheme.textPrimary} opacity-70`}`}>Scegli come vuoi premiare il tuo impegno!</p>
            </div>
            <button
              onClick={() => setIsConfigured(true)}
              className={`w-full md:w-auto px-6 py-3 md:px-8 md:py-4 rounded-xl md:rounded-2xl font-black text-base md:text-lg flex items-center justify-center gap-2 transition-all shadow-lg active:scale-95 ${isDarkMode ? 'bg-emerald-600 text-white hover:bg-emerald-700' : 'bg-emerald-400 text-white hover:bg-emerald-500 hover:scale-105 shadow-emerald-200'}`}
            >
              <Save size={20} className="md:w-6 md:h-6" /> SALVA ORA
            </button>
          </header>

          {/* Category Info Cards */}
          <div className="grid grid-cols-1 sm:grid-cols-3 gap-3 md:gap-6 mb-6 md:mb-10">
            <motion.div whileHover={{ y: -5 }} className={`p-4 md:p-6 rounded-[1.5rem] md:rounded-[2rem] shadow-lg border-b-4 md:border-b-8 ${isDarkMode ? 'bg-slate-900 border-slate-800' : 'bg-white border-slate-200'}`}>
              <div className={`w-10 h-10 md:w-12 md:h-12 rounded-xl md:rounded-2xl flex items-center justify-center mb-3 md:mb-4 ${isDarkMode ? 'bg-slate-800 text-slate-500' : 'bg-slate-100 text-slate-500'}`}>
                <BookOpen size={24} className="md:w-7 md:h-7" />
              </div>
              <h3 className={`font-black text-lg md:text-xl mb-1 ${isDarkMode ? 'text-white' : 'text-slate-700'}`}>Standard</h3>
              <p className={`text-xs md:text-sm font-medium ${isDarkMode ? 'text-slate-500' : 'text-slate-400'}`}>Le solite regole, equilibrate e giuste!</p>
            </motion.div>
            <motion.div whileHover={{ y: -5 }} className={`p-4 md:p-6 rounded-[1.5rem] md:rounded-[2rem] shadow-lg border-b-4 md:border-b-8 ${isDarkMode ? 'bg-slate-900 border-amber-900/50' : 'bg-white border-amber-200'}`}>
              <div className={`w-10 h-10 md:w-12 md:h-12 rounded-xl md:rounded-2xl flex items-center justify-center mb-3 md:mb-4 ${isDarkMode ? 'bg-amber-900/30 text-amber-500' : 'bg-amber-100 text-amber-500'}`}>
                <Sparkles size={24} className="md:w-7 md:h-7" />
              </div>
              <h3 className={`font-black text-lg md:text-xl mb-1 ${isDarkMode ? 'text-amber-400' : 'text-amber-700'}`}>Talento</h3>
              <p className={`text-xs md:text-sm font-medium ${isDarkMode ? 'text-amber-600/60' : 'text-amber-400'}`}>Qui si punta in alto! Solo i migliori vincono.</p>
            </motion.div>
            <motion.div whileHover={{ y: -5 }} className={`p-4 md:p-6 rounded-[1.5rem] md:rounded-[2rem] shadow-lg border-b-4 md:border-b-8 ${isDarkMode ? 'bg-slate-900 border-emerald-900/50' : 'bg-white border-emerald-200'}`}>
              <div className={`w-10 h-10 md:w-12 md:h-12 rounded-xl md:rounded-2xl flex items-center justify-center mb-3 md:mb-4 ${isDarkMode ? 'bg-emerald-900/30 text-emerald-500' : 'bg-emerald-100 text-emerald-500'}`}>
                <Zap size={24} className="md:w-7 md:h-7" />
              </div>
              <h3 className={`font-black text-lg md:text-xl mb-1 ${isDarkMode ? 'text-emerald-400' : 'text-emerald-700'}`}>Sforzo</h3>
              <p className={`text-xs md:text-sm font-medium ${isDarkMode ? 'text-emerald-600/60' : 'text-emerald-400'}`}>Premia la tua grinta! Ogni passo conta.</p>
            </motion.div>
          </div>

          {/* Subject List */}
          <div className={`rounded-[1.5rem] md:rounded-[2.5rem] shadow-xl border-2 overflow-hidden ${isDarkMode ? 'bg-slate-900 border-slate-800 shadow-black/20' : `bg-white ${currentTheme.borderSecondary50} ${currentTheme.shadowGlow}`}`}>
            <div className={`divide-y-2 ${isDarkMode ? 'divide-slate-800' : currentTheme.borderSecondary50}`}>
              {subjects.map(s => (
                <div key={s.name} className={`px-4 md:px-10 py-4 md:py-6 flex flex-col sm:flex-row sm:items-center justify-between gap-3 md:gap-4 transition-colors ${isDarkMode ? 'hover:bg-slate-800/30' : `hover:${currentTheme.bgSecondary50}`}`}>
                  <span className={`text-lg md:text-2xl font-black ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>{s.name}</span>
                  <div className={`flex flex-wrap sm:flex-nowrap gap-1.5 md:gap-3 p-1.5 md:p-2 rounded-2xl md:rounded-3xl ${isDarkMode ? 'bg-slate-800/50' : currentTheme.bgSecondary50}`}>
                    <button
                      onClick={() => handleTypeChange(s.name, 'Standard')}
                      className={`flex-1 sm:flex-none flex items-center justify-center gap-2 px-3 md:px-6 py-2 md:py-3 rounded-xl md:rounded-2xl text-[10px] md:text-sm font-black transition-all ${
                        s.type === 'Standard'
                        ? (isDarkMode ? 'bg-slate-700 shadow-md text-white scale-105' : 'bg-white shadow-md text-slate-600 scale-105')
                        : (isDarkMode ? 'text-slate-500 hover:text-slate-400' : 'text-slate-400 hover:text-slate-600')
                      }`}
                    >
                      <BookOpen size={14} className="md:w-4 md:h-4" /> Standard
                    </button>
                    <button
                      onClick={() => handleTypeChange(s.name, 'Talento')}
                      className={`flex-1 sm:flex-none flex items-center justify-center gap-2 px-3 md:px-6 py-2 md:py-3 rounded-xl md:rounded-2xl text-[10px] md:text-sm font-black transition-all ${
                        s.type === 'Talento'
                        ? 'bg-amber-400 shadow-md text-white scale-105'
                        : 'text-amber-600/60 hover:text-amber-700'
                      }`}
                    >
                      <Sparkles size={14} className="md:w-4 md:h-4" /> Talento
                    </button>
                    <button
                      onClick={() => handleTypeChange(s.name, 'Sforzo')}
                      className={`flex-1 sm:flex-none flex items-center justify-center gap-2 px-3 md:px-6 py-2 md:py-3 rounded-xl md:rounded-2xl text-[10px] md:text-sm font-black transition-all ${
                        s.type === 'Sforzo'
                        ? 'bg-emerald-400 shadow-md text-white scale-105'
                        : 'text-emerald-600/60 hover:text-emerald-700'
                      }`}
                    >
                      <Zap size={14} className="md:w-4 md:h-4" /> Sforzo
                    </button>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </div>
    );
  }
  const addGrade = (subjectName: string, semester: Semester, gradeLabel: string) => {
    const gradeValue = GRADE_MAP[gradeLabel];
    if (gradeValue === undefined) return;

    setSubjects(prev => prev.map(s => {
      if (s.name === subjectName) {
        const newGrade: Grade = {
          id: Math.random().toString(36).substr(2, 9),
          value: gradeValue,
          label: gradeLabel,
          timestamp: Date.now()
        };
        return {
          ...s,
          grades: {
            ...s.grades,
            [semester]: [...s.grades[semester], newGrade]
          }
        };
      }
      return s;
    }));
    setLastSelectedSubject(subjectName);
    setLastSelectedSemester(semester);
  };

  const removeLastGrade = (subjectName: string, semester: Semester) => {
    setSubjects(prev => prev.map(s => {
      if (s.name === subjectName) {
        return {
          ...s,
          grades: {
            ...s.grades,
            [semester]: s.grades[semester].slice(0, -1)
          }
        };
      }
      return s;
    }));
  };

  const resetAll = () => {
    setSubjects(PREDEFINED_SUBJECTS.map(name => ({
      name,
      type: 'Standard',
      grades: { Q1: [], Q2: [] }
    })));
    setIsConfigured(false);
    setShowResetConfirm(false);
    localStorage.removeItem('grade_rewards_data');
  };

  const exportReport = () => {
    const report = {
      date: new Date().toLocaleDateString(),
      totalBalance: stats.totalBalance,
      status: stats.isFrozen ? 'CONGELATO' : 'DISPONIBILE',
      subjects: stats.subjectStats.map(s => ({
        materia: s.name,
        tipo: s.type,
        media: s.avg.toFixed(2),
        guadagno: s.totalReward + '€',
        votiQ1: s.grades.Q1.map(g => g.label).join(', '),
        votiQ2: s.grades.Q2.map(g => g.label).join(', ')
      }))
    };

    const blob = new Blob([JSON.stringify(report, null, 2)], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `report_voti_${new Date().toISOString().split('T')[0]}.json`;
    a.click();
  };


  // Main Dashboard
  return (
    <div className={`min-h-screen font-sans transition-all duration-700 selection:bg-slate-200 ${isDarkMode ? 'bg-slate-950 text-slate-300' : `bg-gradient-to-br ${currentTheme.gradient} text-slate-900`}`}>
      {/* Background Glows */}
      <div className="fixed inset-0 overflow-hidden pointer-events-none">
        <div className={`absolute -top-[10%] -left-[10%] w-[40%] h-[40%] rounded-full blur-[120px] opacity-20 ${isDarkMode ? currentTheme.bgPrimaryDark : currentTheme.bgPrimary}`} />
        <div className={`absolute -bottom-[10%] -right-[10%] w-[40%] h-[40%] rounded-full blur-[120px] opacity-20 ${isDarkMode ? 'bg-slate-900' : currentTheme.bgSecondary}`} />
      </div>

      {/* Top Navigation / Stats */}
      <nav className="sticky top-2 md:top-4 z-20 mx-2 md:mx-6 my-2 md:my-4">
        <div className={`max-w-7xl mx-auto backdrop-blur-xl border-2 rounded-[1.5rem] md:rounded-[2rem] shadow-2xl px-4 md:px-8 py-3 md:py-4 flex items-center justify-between gap-3 md:gap-4 transition-all ${isDarkMode ? 'bg-slate-900/80 border-slate-800/50 shadow-black/20' : `bg-white/70 ${currentTheme.borderSecondary50} ${currentTheme.shadowGlow}`}`}>
          <div className="flex items-center gap-2 md:gap-4 group cursor-pointer">
            <div className={`w-9 h-9 md:w-12 md:h-12 bg-gradient-to-tr ${currentTheme.fromPrimary} ${currentTheme.toAccent} rounded-xl md:rounded-2xl flex items-center justify-center text-white shadow-lg transition-all group-hover:scale-110 group-hover:rotate-6 ${currentTheme.shadowGlow}`}>
              <Award size={20} className="md:w-7 md:h-7" />
            </div>
            <div className="hidden sm:block">
              <h1 className={`text-lg md:text-2xl font-black tracking-tight leading-tight ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>GradeRewards</h1>
              <p className={`text-[8px] md:text-[10px] font-bold uppercase tracking-widest ${isDarkMode ? 'text-slate-500' : `${currentTheme.textPrimary} opacity-80`}`}>Il tuo salvadanaio scolastico</p>
            </div>
            <div className="sm:hidden">
              <h1 className={`text-base font-black tracking-tight leading-tight ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>GR</h1>
            </div>
          </div>

          {/* Overall Averages and Potential Bonus */}
          <div className="hidden lg:flex items-center gap-6 px-6 border-x-2 border-slate-100/10">
            <div className="flex flex-col items-center">
              <span className={`text-[8px] uppercase font-black tracking-widest ${isDarkMode ? 'text-slate-500' : 'text-slate-400'}`}>Media Q1</span>
              <span className={`text-sm font-black ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>{stats.overallAvgQ1.toFixed(2)}</span>
            </div>
            <div className="flex flex-col items-center">
              <span className={`text-[8px] uppercase font-black tracking-widest ${isDarkMode ? 'text-slate-500' : 'text-slate-400'}`}>Media Q2</span>
              <span className={`text-sm font-black ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>{stats.overallAvgQ2.toFixed(2)}</span>
            </div>
            {stats.improvementBonus > 0 && (
              <div className={`flex flex-col items-center px-3 py-1 rounded-xl shadow-sm border transition-all hover:scale-105 ${isDarkMode ? 'bg-emerald-900/30 text-emerald-400 border-emerald-800/50' : 'bg-emerald-50 text-emerald-700 border-emerald-100'}`}>
                <span className="text-[7px] uppercase font-black tracking-tighter">Bonus Miglioramento</span>
                <span className="text-[10px] font-black">+{stats.improvementBonus.toFixed(2)}€ <span className="opacity-60 text-[8px]">(Potenziale)</span></span>
              </div>
            )}
          </div>

          <div className="flex items-center gap-3 md:gap-8">
            <div className="flex flex-col items-end">
              <span className={`text-[7px] md:text-[10px] uppercase tracking-widest font-black ${isDarkMode ? 'text-slate-500' : `${currentTheme.textPrimary} opacity-60`}`}>Tesoretto Accumulato</span>
              <div className="flex items-center gap-2 md:gap-3">
                <div className={`text-xl md:text-3xl font-black tracking-tighter ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>
                  {stats.totalBalance.toFixed(2)}€
                </div>
                <div className={`p-1 md:p-2 rounded-lg md:rounded-xl shadow-lg transition-all ${stats.isFrozen ? 'bg-rose-500 text-white animate-bounce shadow-rose-500/20' : isDarkMode ? `bg-slate-800 ${currentTheme.textPrimaryDark} ${currentTheme.shadowPrimaryDark}` : `${currentTheme.bgSecondary} ${currentTheme.textPrimary} ${currentTheme.shadowGlow}`}`}>
                  {stats.isFrozen ? <Lock size={14} className="md:w-5 md:h-5" /> : <Unlock size={14} className="md:w-5 md:h-5" />}
                </div>
              </div>
              {stats.improvementBonus > 0 && (
                <span className={`lg:hidden text-[7px] font-black uppercase mt-1 ${isDarkMode ? 'text-emerald-400' : 'text-emerald-600'}`}>
                  + {stats.improvementBonus.toFixed(2)}€ Potenziale
                </span>
              )}
            </div>
            
            <button 
              onClick={() => setIsSettingsOpen(true)}
              className={`p-2 md:p-3 rounded-xl md:rounded-2xl transition-all shadow-lg ${isDarkMode ? 'bg-slate-800 text-slate-400 hover:text-white hover:bg-slate-700 shadow-black/20' : `${currentTheme.bgSecondary} ${currentTheme.textPrimary} hover:scale-110 ${currentTheme.shadowGlow}`}`}
            >
              <Settings2 size={18} className="md:w-6 md:h-6" />
            </button>
          </div>
        </div>
      </nav>

      <main className="max-w-7xl mx-auto p-3 md:p-6 grid grid-cols-1 md:grid-cols-12 gap-4 md:gap-8">
        
        {/* Left Column: Grade Entry & Actions */}
        <div className="md:col-span-5 lg:col-span-4 space-y-4 md:space-y-8 md:sticky md:top-28 self-start">
          <section className={`p-5 md:p-8 rounded-[1.5rem] md:rounded-[2.5rem] shadow-2xl border-2 transition-all ${isDarkMode ? 'bg-slate-900 border-slate-800 shadow-black/20' : `bg-white ${currentTheme.borderSecondary50} ${currentTheme.shadowGlow}`}`}>
            <h2 className={`text-base md:text-xl font-black mb-4 md:mb-6 flex items-center gap-3 ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>
              <div className={`p-1.5 md:p-2 rounded-lg md:rounded-xl shadow-lg ${isDarkMode ? `bg-slate-800 ${currentTheme.textPrimaryDark} ${currentTheme.shadowPrimaryDark}` : `${currentTheme.bgSecondary} ${currentTheme.textPrimary} ${currentTheme.shadowGlow}`}`}><Plus size={18} className="md:w-6 md:h-6" /></div> 
              Nuovo Voto! 🚀
            </h2>
            <div className="space-y-4 md:space-y-6">
              <div className="relative">
                <label className={`text-[9px] md:text-xs font-black uppercase mb-1.5 md:mb-2 block ml-1 ${isDarkMode ? 'text-slate-500' : `${currentTheme.textPrimary} opacity-60`}`}>Quale materia?</label>
                <button 
                  onClick={() => setIsSubjectDropdownOpen(!isSubjectDropdownOpen)}
                  className={`w-full border-2 border-transparent rounded-xl md:rounded-2xl p-3 md:p-4 font-bold flex items-center justify-between transition-all text-sm md:text-base ${isDarkMode ? 'bg-slate-800 text-white hover:border-slate-700' : `${currentTheme.bgSecondary50} ${currentTheme.textAccent} hover:${currentTheme.borderSecondary}`}`}
                >
                  <span className="truncate">{lastSelectedSubject || (subjects.length > 0 ? subjects[0].name : '')}</span>
                  <motion.div
                    animate={{ rotate: isSubjectDropdownOpen ? 180 : 0 }}
                    transition={{ type: "spring", stiffness: 300, damping: 20 }}
                  >
                    <ChevronDown size={16} className={`md:w-5 md:h-5 ${isDarkMode ? 'text-slate-500' : `${currentTheme.textPrimary} opacity-70`}`} />
                  </motion.div>
                </button>

                <AnimatePresence>
                  {isSubjectDropdownOpen && (
                    <>
                      {/* Backdrop to close dropdown */}
                      <div 
                        className="fixed inset-0 z-30" 
                        onClick={() => setIsSubjectDropdownOpen(false)} 
                      />
                      <motion.div
                        initial={{ opacity: 0, y: -10, scale: 0.95 }}
                        animate={{ opacity: 1, y: 5, scale: 1 }}
                        exit={{ opacity: 0, y: -10, scale: 0.95 }}
                        className={`absolute left-0 right-0 z-40 border-2 rounded-[2rem] shadow-2xl overflow-hidden py-2 ${isDarkMode ? 'bg-slate-900 border-slate-800 shadow-black/40' : `bg-white ${currentTheme.borderSecondary} ${currentTheme.shadowPrimary20}`}`}
                      >
                        <div className="max-h-[300px] overflow-y-auto custom-scrollbar">
                          {subjects.map(s => (
                            <button
                              key={s.name}
                              onClick={() => {
                                setLastSelectedSubject(s.name);
                                setIsSubjectDropdownOpen(false);
                              }}
                              className={`w-full text-left px-6 py-3 font-bold text-sm transition-colors flex items-center justify-between ${
                                (lastSelectedSubject || subjects[0].name) === s.name 
                                ? (isDarkMode ? `${currentTheme.bgPrimarySolidDark} text-white` : `${currentTheme.bgPrimary} text-white`)
                                : (isDarkMode ? 'text-slate-300 hover:bg-slate-800' : `${currentTheme.textAccent} hover:${currentTheme.bgSecondary50}`)
                              }`}
                            >
                              {s.name}
                              {(lastSelectedSubject || subjects[0].name) === s.name && (
                                <div className="w-2 h-2 bg-white rounded-full shadow-sm" />
                              )}
                            </button>
                          ))}
                        </div>
                      </motion.div>
                    </>
                  )}
                </AnimatePresence>
              </div>

              <div>
                <label className={`text-[10px] md:text-xs font-black uppercase mb-2 block ml-1 ${isDarkMode ? 'text-slate-500' : `${currentTheme.textPrimary} opacity-60`}`}>Quando?</label>
                <div className={`flex gap-2 md:gap-3 p-1 md:p-1.5 rounded-xl md:rounded-2xl ${isDarkMode ? 'bg-slate-800' : currentTheme.bgSecondary50}`}>
                  {(['Q1', 'Q2'] as Semester[]).map(q => (
                    <button
                      key={q}
                      onClick={() => setLastSelectedSemester(q)}
                      className={`flex-1 py-2 md:py-3 rounded-lg md:rounded-xl font-black text-xs md:text-sm transition-all ${
                        lastSelectedSemester === q 
                        ? (isDarkMode ? 'bg-slate-700 shadow-md text-white scale-105' : `bg-white shadow-md ${currentTheme.textPrimary} scale-105`)
                        : (isDarkMode ? 'text-slate-500 hover:text-slate-400' : (isDarkMode ? 'text-slate-500' : `${currentTheme.textPrimary} opacity-60 hover:opacity-100`))
                      }`}
                    >
                      {q === 'Q1' ? '1° Quad' : '2° Quad'}
                    </button>
                  ))}
                </div>
              </div>

              <div>
                <label className={`text-[9px] md:text-xs font-black uppercase mb-2 md:mb-3 block ml-1 ${isDarkMode ? 'text-slate-500' : `${currentTheme.textPrimary} opacity-60`}`}>Scegli il voto:</label>
                <div className="grid grid-cols-4 sm:grid-cols-6 md:grid-cols-4 lg:grid-cols-4 gap-1.5 md:gap-2">
                  {Object.keys(GRADE_MAP)
                    .sort((a, b) => GRADE_MAP[a] - GRADE_MAP[b])
                    .map(label => {
                      const val = GRADE_MAP[label];
                      let colorClass = isDarkMode 
                        ? "bg-rose-900/30 text-rose-400 hover:bg-rose-900/50" 
                        : "bg-rose-50 text-rose-500 hover:bg-rose-100";
                      
                      if (val >= 8) colorClass = isDarkMode 
                        ? "bg-emerald-900/30 text-emerald-400 hover:bg-emerald-900/50" 
                        : "bg-emerald-50 text-emerald-700 hover:bg-emerald-100";
                      else if (val >= 6) colorClass = isDarkMode 
                        ? `${currentTheme.bgPrimaryDark} ${currentTheme.textPrimaryDark} hover:bg-opacity-50` 
                        : `${currentTheme.bgSecondary} ${currentTheme.textPrimary} hover:bg-opacity-80`;
                      else if (val >= 5) colorClass = isDarkMode 
                        ? "bg-amber-900/30 text-amber-400 hover:bg-amber-900/50" 
                        : "bg-amber-50 text-amber-600 hover:bg-amber-100";

                      // Dynamic scale based on grade: 1.0 for < 6, up to 1.25 for 10
                      const hoverScale = val >= 6 ? 1.1 + ((val - 6) / 4) * 0.15 : 1.1;

                      return (
                        <GradeButton
                          key={label}
                          label={label}
                          val={val}
                          colorClass={colorClass}
                          hoverScale={hoverScale}
                          isDarkMode={isDarkMode}
                          onClick={() => addGrade(lastSelectedSubject || subjects[0].name, lastSelectedSemester, label)}
                        />
                      );
                    })}
                </div>
              </div>
            </div>
          </section>

          <section className={`p-4 md:p-6 rounded-[2rem] md:rounded-[2.5rem] shadow-xl border-2 space-y-3 ${isDarkMode ? 'bg-slate-900 border-slate-800 shadow-black/20' : `bg-white ${currentTheme.borderSecondary50} ${currentTheme.shadowGlow}`}`}>
            <button 
              onClick={exportReport}
              className={`w-full flex items-center justify-center gap-3 py-3 md:py-4 text-white rounded-xl md:rounded-2xl font-black text-xs md:text-sm transition-all shadow-lg ${isDarkMode ? `${currentTheme.bgPrimarySolidDark} hover:opacity-90 ${currentTheme.shadowPrimaryDark}` : `${currentTheme.bgPrimary} hover:opacity-90 ${currentTheme.shadowPrimary20}`}`}
            >
              <Download size={18} md:size={20} /> SCARICA REPORT
            </button>
            <div className="grid grid-cols-2 gap-2 md:gap-3">
              <button 
                onClick={() => setIsConfigured(false)}
                className={`flex items-center justify-center gap-2 py-2.5 md:py-3 rounded-xl md:rounded-2xl font-bold text-[10px] md:text-xs transition-all ${isDarkMode ? 'bg-slate-800 text-slate-300 hover:bg-slate-700' : 'bg-slate-100 text-slate-600 hover:bg-slate-200'}`}
              >
                <Settings2 size={14} md:size={16} /> SETUP
              </button>
              <button 
                onClick={() => setShowResetConfirm(true)}
                className={`flex items-center justify-center gap-2 py-2.5 md:py-3 rounded-xl md:rounded-2xl font-bold text-[10px] md:text-xs transition-all ${isDarkMode ? 'bg-rose-900/20 text-rose-400 hover:bg-rose-900/30' : 'bg-rose-50 text-rose-500 hover:bg-rose-100'}`}
              >
                <RotateCcw size={14} md:size={16} /> RESET
              </button>
            </div>
          </section>
        </div>

        {/* Right Column: Summary Table */}
        <div className="md:col-span-7 lg:col-span-8">
          <div className={`rounded-[1.5rem] md:rounded-[3rem] shadow-2xl border-2 overflow-hidden transition-all ${isDarkMode ? 'bg-slate-900 border-slate-800 shadow-black/20' : `bg-white ${currentTheme.borderSecondary50} ${currentTheme.shadowGlow}`}`}>
            <div className={`p-4 md:p-8 border-b-2 flex flex-col sm:flex-row sm:items-center justify-between gap-4 ${isDarkMode ? 'border-slate-800 bg-slate-900/50' : `${currentTheme.borderSecondary50} bg-gradient-to-r from-white ${currentTheme.toSecondary30}`}`}>
              <h2 className={`text-lg md:text-2xl font-black flex items-center gap-3 ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>
                <div className={`p-1.5 md:p-2 rounded-lg md:rounded-2xl text-white shadow-lg ${isDarkMode ? `${currentTheme.bgPrimarySolidDark} ${currentTheme.shadowPrimaryDark}` : `${currentTheme.bgPrimary} ${currentTheme.shadowGlow}`}`}><History size={18} className="md:w-6 md:h-6" /></div> 
                I Tuoi Successi 🏆
              </h2>
              {stats.isFrozen && (
                <div className={`flex items-center gap-2 text-white px-3 py-1.5 md:px-4 md:py-2 rounded-full text-[9px] md:text-[10px] font-black animate-pulse shadow-lg ${isDarkMode ? 'bg-rose-600 shadow-rose-900/20' : 'bg-rose-500 shadow-rose-200'}`}>
                  <AlertCircle size={12} className="md:w-3.5 md:h-3.5" /> SALDO CONGELATO
                </div>
              )}
            </div>
            
            <div className="overflow-x-auto custom-scrollbar">
              <table className="w-full text-left border-collapse min-w-[500px] md:min-w-0">
                <thead>
                  <tr className={`text-[8px] md:text-[10px] uppercase tracking-widest font-black ${isDarkMode ? 'bg-slate-800/50 text-slate-500' : `${currentTheme.bgSecondary50} ${currentTheme.textPrimary}`}`}>
                    <th className="px-3 md:px-8 py-3 md:py-5 sticky left-0 z-10 bg-inherit shadow-[2px_0_5px_-2px_rgba(0,0,0,0.1)] md:shadow-none">Materia</th>
                    <th className="px-3 md:px-8 py-3 md:py-5">1° Quad</th>
                    <th className="px-3 md:px-8 py-3 md:py-5">2° Quad</th>
                    <th className="px-3 md:px-8 py-3 md:py-5">Media</th>
                    <th className="px-3 md:px-8 py-3 md:py-5 text-right">Premi</th>
                  </tr>
                </thead>
                <tbody className={`divide-y-2 ${isDarkMode ? 'divide-slate-800' : currentTheme.borderSecondary50}`}>
                  {stats.subjectStats.map(s => (
                    <tr key={s.name} className={`transition-colors group ${isDarkMode ? 'hover:bg-slate-800/20' : `${currentTheme.bgSecondary50} hover:bg-white/50`}`}>
                      <td className="px-3 md:px-8 py-3 md:py-6 sticky left-0 z-10 bg-inherit shadow-[2px_0_5px_-2px_rgba(0,0,0,0.1)] md:shadow-none">
                        <div className="flex flex-col">
                          <span className={`font-black text-sm md:text-lg ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>{s.name}</span>
                          <div className="flex items-center gap-1">
                            <span className={`w-1.5 h-1.5 md:w-2 md:h-2 rounded-full shadow-sm ${
                              s.type === 'Talento' ? 'bg-amber-400 shadow-amber-400/50' : 
                              s.type === 'Sforzo' ? 'bg-emerald-400 shadow-emerald-400/50' : 'bg-slate-300'
                            }`} />
                            <span className={`text-[7px] md:text-[10px] font-black uppercase tracking-wider ${
                              s.type === 'Talento' ? 'text-amber-600' : 
                              s.type === 'Sforzo' ? 'text-emerald-600' : 'text-slate-500'
                            }`}>
                              {s.type}
                            </span>
                          </div>
                        </div>
                      </td>
                      <td className="px-3 md:px-8 py-3 md:py-6">
                        <div className="flex flex-col gap-1.5">
                          <div className="flex flex-wrap gap-1 md:gap-1.5 items-center">
                            {s.grades.Q1.map(g => (
                              <div key={g.id} className="relative group/grade">
                                <span className={`px-1.5 py-0.5 md:px-2.5 md:py-1 rounded-md md:rounded-lg text-[8px] md:text-[11px] font-black shadow-sm cursor-help ${
                                  g.value >= 6 
                                    ? (isDarkMode ? 'bg-emerald-900/40 text-emerald-400' : 'bg-emerald-100 text-emerald-700') 
                                    : (isDarkMode ? 'bg-rose-900/40 text-rose-400' : 'bg-rose-100 text-rose-700')
                                }`}>
                                  {g.label}
                                </span>
                                <div className="absolute bottom-full left-1/2 -translate-x-1/2 mb-2 hidden group-hover/grade:block z-50 pointer-events-none">
                                  <div className={`px-2 py-1 rounded text-[11px] font-bold whitespace-nowrap shadow-xl border ${
                                    isDarkMode ? 'bg-slate-800 text-white border-slate-700' : 'bg-white text-slate-800 border-slate-200'
                                  }`}>
                                    {formatDate(g.timestamp)}
                                  </div>
                                  <div className={`w-2 h-2 rotate-45 absolute -bottom-1 left-1/2 -translate-x-1/2 border-r border-b ${
                                    isDarkMode ? 'bg-slate-800 border-slate-700' : 'bg-white border-slate-200'
                                  }`} />
                                </div>
                              </div>
                            ))}
                            {s.grades.Q1.length > 0 && (
                              <button 
                                onClick={() => removeLastGrade(s.name, 'Q1')}
                                className={`opacity-0 group-hover:opacity-100 p-1 md:p-1.5 transition-all rounded-lg ${isDarkMode ? 'text-rose-400 bg-rose-900/20 hover:bg-rose-900/40' : 'text-rose-300 hover:text-rose-500 bg-rose-50'}`}
                              >
                                <Trash2 size={10} className="md:w-3.5 md:h-3.5" />
                              </button>
                            )}
                          </div>
                          {s.q1Avg > 0 && (
                            <div className={`text-[7px] md:text-[9px] font-bold opacity-60 ${isDarkMode ? 'text-slate-400' : 'text-slate-500'}`}>
                              Media: {s.q1Avg.toFixed(2)}
                            </div>
                          )}
                        </div>
                      </td>
                      <td className="px-3 md:px-8 py-3 md:py-6">
                        <div className="flex flex-col gap-1.5">
                          <div className="flex flex-wrap gap-1 md:gap-1.5 items-center">
                            {s.grades.Q2.map(g => (
                              <div key={g.id} className="relative group/grade">
                                <span className={`px-1.5 py-0.5 md:px-2.5 md:py-1 rounded-md md:rounded-lg text-[8px] md:text-[11px] font-black shadow-sm cursor-help ${
                                  g.value >= 6 
                                    ? (isDarkMode ? 'bg-emerald-900/40 text-emerald-400' : 'bg-emerald-100 text-emerald-700') 
                                    : (isDarkMode ? 'bg-rose-900/40 text-rose-400' : 'bg-rose-100 text-rose-700')
                                }`}>
                                  {g.label}
                                </span>
                                <div className="absolute bottom-full left-1/2 -translate-x-1/2 mb-2 hidden group-hover/grade:block z-50 pointer-events-none">
                                  <div className={`px-2 py-1 rounded text-[11px] font-bold whitespace-nowrap shadow-xl border ${
                                    isDarkMode ? 'bg-slate-800 text-white border-slate-700' : 'bg-white text-slate-800 border-slate-200'
                                  }`}>
                                    {formatDate(g.timestamp)}
                                  </div>
                                  <div className={`w-2 h-2 rotate-45 absolute -bottom-1 left-1/2 -translate-x-1/2 border-r border-b ${
                                    isDarkMode ? 'bg-slate-800 border-slate-700' : 'bg-white border-slate-200'
                                  }`} />
                                </div>
                              </div>
                            ))}
                            {s.grades.Q2.length > 0 && (
                              <button 
                                onClick={() => removeLastGrade(s.name, 'Q2')}
                                className={`opacity-0 group-hover:opacity-100 p-1 md:p-1.5 transition-all rounded-lg ${isDarkMode ? 'text-rose-400 bg-rose-900/20 hover:bg-rose-900/40' : 'text-rose-300 hover:text-rose-500 bg-rose-50'}`}
                              >
                                <Trash2 size={10} className="md:w-3.5 md:h-3.5" />
                              </button>
                            )}
                          </div>
                          {s.q2Avg > 0 && (
                            <div className={`text-[7px] md:text-[9px] font-bold opacity-60 ${isDarkMode ? 'text-slate-400' : 'text-slate-500'}`}>
                              Media: {s.q2Avg.toFixed(2)}
                            </div>
                          )}
                        </div>
                      </td>
                      <td className="px-3 md:px-8 py-3 md:py-6">
                        <div className="flex items-center gap-2">
                          <div className={`w-8 h-8 md:w-12 md:h-12 rounded-lg md:rounded-2xl flex items-center justify-center font-black text-[10px] md:text-sm shadow-inner ${
                            s.avg >= 6 
                              ? (isDarkMode ? 'bg-emerald-900/20 text-emerald-400' : 'bg-emerald-50 text-emerald-600') 
                              : s.avg > 0 
                                ? (isDarkMode ? 'bg-rose-900/20 text-rose-400' : 'bg-rose-50 text-rose-600') 
                                : (isDarkMode ? 'bg-slate-800 text-slate-600' : 'bg-slate-50 text-slate-300')
                          }`}>
                            {s.avg > 0 ? s.avg.toFixed(2) : '-'}
                          </div>
                        </div>
                      </td>
                      <td className="px-3 md:px-8 py-3 md:py-6 text-right">
                        <div className="flex flex-col items-end">
                          <span className={`text-sm md:text-lg font-black ${s.totalReward >= 0 ? 'text-emerald-500' : 'text-rose-500'}`}>
                            {s.totalReward.toFixed(2)}€
                          </span>
                          {s.recoveryBonuses > 0 && (
                            <span className={`text-[7px] md:text-[10px] font-black text-emerald-500 bg-emerald-50 px-1.5 py-0.5 rounded-full`}>
                              +{s.recoveryBonuses}€ BONUS! 🎈
                            </span>
                          )}
                          {s.improvementBonus > 0 && (
                            <span className={`text-[7px] md:text-[10px] font-black text-emerald-500 mt-1 flex items-center gap-1`}>
                              <TrendingUp size={10} /> +{s.improvementBonus}€ Miglioramento
                            </span>
                          )}
                        </div>
                      </td>
                    </tr>
                  ))}
                </tbody>
                <tfoot className={`border-t-4 ${isDarkMode ? 'border-slate-800 bg-slate-900/50' : `${currentTheme.borderSecondary50} bg-slate-50/30`}`}>
                  <tr className="text-[9px] md:text-[11px] font-black uppercase tracking-widest">
                    <td className="px-3 md:px-8 py-4 sticky left-0 z-10 bg-inherit shadow-[2px_0_5px_-2px_rgba(0,0,0,0.1)] md:shadow-none">Media Totale</td>
                    <td className="px-3 md:px-8 py-4">
                      <span className={isDarkMode ? 'text-white' : currentTheme.textAccent}>{stats.overallAvgQ1 > 0 ? stats.overallAvgQ1.toFixed(2) : '-'}</span>
                    </td>
                    <td className="px-3 md:px-8 py-4">
                      <span className={isDarkMode ? 'text-white' : currentTheme.textAccent}>{stats.overallAvgQ2 > 0 ? stats.overallAvgQ2.toFixed(2) : '-'}</span>
                    </td>
                    <td className="px-3 md:px-8 py-4">
                      <span className={isDarkMode ? 'text-white' : currentTheme.textAccent}>
                        {stats.overallAvgTotal > 0 ? stats.overallAvgTotal.toFixed(2) : '-'}
                      </span>
                    </td>
                    <td className="px-3 md:px-8 py-4 text-right">
                      {stats.improvementBonus > 0 && (
                        <span className="text-emerald-500">+{stats.improvementBonus.toFixed(2)}€ Potenziale</span>
                      )}
                    </td>
                  </tr>
                </tfoot>
              </table>
            </div>
          </div>
        </div>
      </main>

      {/* Settings Modal */}
      <AnimatePresence>
        {isSettingsOpen && (
          <motion.div 
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            className="fixed inset-0 z-50 bg-slate-900/40 backdrop-blur-sm flex items-center justify-center p-6"
          >
            <motion.div 
              initial={{ scale: 0.9, opacity: 0, y: 20 }}
              animate={{ scale: 1, opacity: 1, y: 0 }}
              exit={{ scale: 0.9, opacity: 0, y: 20 }}
              className={`rounded-[2rem] md:rounded-[3rem] p-6 md:p-8 max-w-md w-full shadow-2xl border-2 transition-all mx-4 ${isDarkMode ? 'bg-slate-900 border-slate-800 shadow-black/40' : `bg-white ${currentTheme.borderSecondary50} ${currentTheme.shadowGlow}`}`}
            >
              <div className="flex items-center justify-between mb-8">
                <h3 className={`text-2xl font-black flex items-center gap-3 ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>
                  <div className={`p-2 rounded-xl shadow-lg ${isDarkMode ? `bg-slate-800 ${currentTheme.textPrimaryDark} ${currentTheme.shadowPrimaryDark}` : `${currentTheme.bgSecondary} ${currentTheme.textPrimary} ${currentTheme.shadowGlow}`}`}><Palette size={24} /></div>
                  Personalizza
                </h3>
                <button 
                  onClick={() => setIsSettingsOpen(false)}
                  className={`p-2 rounded-xl transition-all ${isDarkMode ? 'bg-slate-800 text-slate-400 hover:bg-slate-700' : 'bg-slate-50 text-slate-400 hover:bg-slate-100'}`}
                >
                  <X size={20} />
                </button>
              </div>

              <div className="space-y-8">
                {/* Dark Mode Toggle */}
                <div className="flex items-center justify-between">
                  <div className="flex items-center gap-3">
                    <div className={`p-2 rounded-xl ${isDarkMode ? `${currentTheme.bgPrimaryDark} ${currentTheme.textPrimaryDark}` : 'bg-amber-50 text-amber-500'}`}>
                      {isDarkMode ? <Moon size={20} /> : <Sun size={20} />}
                    </div>
                    <div>
                      <p className={`font-black text-sm ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>Modalità Scura</p>
                      <p className="text-[10px] font-bold text-slate-400 uppercase tracking-wider">Cambia l'atmosfera</p>
                    </div>
                  </div>
                  <button 
                    onClick={() => setIsDarkMode(!isDarkMode)}
                    className={`w-14 h-8 rounded-full p-1 transition-all flex items-center ${isDarkMode ? currentTheme.bgPrimarySolidDark : 'bg-slate-200'}`}
                  >
                    <motion.div 
                      animate={{ x: isDarkMode ? 24 : 0 }}
                      className="w-6 h-6 bg-white rounded-full shadow-sm"
                    />
                  </button>
                </div>

                {/* Theme Selection */}
                <div className="space-y-4">
                  <div className="flex items-center gap-3">
                    <div className={`p-2 rounded-xl ${isDarkMode ? `bg-slate-800 ${currentTheme.textPrimaryDark}` : `${currentTheme.bgSecondary} ${currentTheme.textPrimary}`}`}>
                      <Palette size={20} />
                    </div>
                    <div>
                      <p className={`font-black text-sm ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>
                        Tema Colore: <span className="opacity-60 font-medium">{theme.charAt(0).toUpperCase() + theme.slice(1)}</span>
                      </p>
                      <p className="text-[10px] font-bold text-slate-400 uppercase tracking-wider">Scegli il tuo stile</p>
                    </div>
                  </div>
                  <div className="grid grid-cols-5 gap-3">
                    {Object.entries(THEME_CONFIG).map(([key, config]) => (
                      <button
                        key={key}
                        onClick={() => setTheme(key as Theme)}
                        title={key.charAt(0).toUpperCase() + key.slice(1)}
                        className={`aspect-square rounded-2xl transition-all border-4 flex items-center justify-center ${
                          theme === key 
                            ? (isDarkMode ? 'border-white scale-110 shadow-lg' : `${config.borderPrimary} scale-110 shadow-lg`) 
                            : 'border-transparent hover:scale-105 opacity-70 hover:opacity-100'
                        } bg-gradient-to-br ${config.fromPrimary} ${config.toAccent}`}
                      >
                        {theme === key && <div className="w-3 h-3 bg-white rounded-full shadow-md" />}
                      </button>
                    ))}
                  </div>
                </div>
              </div>
            </motion.div>
          </motion.div>
        )}
      </AnimatePresence>

      {/* Reset Confirmation Overlay */}
      <AnimatePresence>
        {showResetConfirm && (
          <motion.div 
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            className="fixed inset-0 z-50 bg-slate-900/40 backdrop-blur-sm flex items-center justify-center p-6"
          >
            <motion.div 
              initial={{ scale: 0.9, opacity: 0 }}
              animate={{ scale: 1, opacity: 1 }}
              exit={{ scale: 0.9, opacity: 0 }}
              className={`rounded-[2rem] md:rounded-[3rem] p-6 md:p-8 max-w-md w-full shadow-2xl text-center border-2 transition-all ${isDarkMode ? 'bg-slate-900 border-slate-800 shadow-black/40' : `bg-white ${currentTheme.borderSecondary50} ${currentTheme.shadowGlow}`}`}
            >
              <div className={`w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-6 shadow-lg ${isDarkMode ? 'bg-rose-900/30 text-rose-400 shadow-rose-900/20' : 'bg-rose-100 text-rose-600 shadow-rose-200'}`}>
                <RotateCcw size={32} />
              </div>
              <h3 className={`text-2xl font-black mb-2 ${isDarkMode ? 'text-white' : currentTheme.textAccent}`}>Sei sicuro?</h3>
              <p className={`text-sm font-bold mb-8 ${isDarkMode ? 'text-slate-500' : 'text-slate-400'}`}>Questa azione cancellerà permanentemente tutti i voti e le configurazioni salvate. Non potrai tornare indietro.</p>
              <div className="flex gap-3">
                <button 
                  onClick={() => setShowResetConfirm(false)}
                  className={`flex-1 py-4 rounded-2xl font-black text-sm transition-all ${isDarkMode ? 'bg-slate-800 text-slate-400 hover:bg-slate-700' : 'bg-slate-50 text-slate-400 hover:bg-slate-100'}`}
                >
                  Annulla
                </button>
                <button 
                  onClick={resetAll}
                  className={`flex-1 py-4 bg-rose-600 hover:bg-rose-700 text-white rounded-2xl font-black text-sm shadow-lg shadow-rose-200 transition-all`}
                >
                  Sì, Reset
                </button>
              </div>
            </motion.div>
          </motion.div>
        )}
      </AnimatePresence>

      {/* Footer */}
      <footer className={`max-w-7xl mx-auto p-8 text-center text-[10px] font-black uppercase tracking-[0.2em] ${isDarkMode ? 'text-slate-700' : 'text-slate-300'}`}>
        GradeRewards &copy; 2026 • Sistema di Incentivazione Scolastica • Made with 💜
      </footer>
    </div>
  );
}

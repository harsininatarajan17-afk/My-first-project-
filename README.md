# My-first-project-
import React, { useState, useRef, useEffect } from 'react';
import { Camera, Upload, Leaf, AlertCircle, CheckCircle, Globe, Download, Wifi, WifiOff } from 'lucide-react';

const PlantDiseaseAnalyzer = () => {
  const [image, setImage] = useState(null);
  const [analyzing, setAnalyzing] = useState(false);
  const [result, setResult] = useState(null);
  const [language, setLanguage] = useState('en');
  const [isOffline, setIsOffline] = useState(!navigator.onLine);
  const [savedAnalyses, setSavedAnalyses] = useState([]);
  const fileInputRef = useRef(null);
  const cameraInputRef = useRef(null);

  // Monitor online/offline status
  useEffect(() => {
    const handleOnline = () => setIsOffline(false);
    const handleOffline = () => setIsOffline(true);
    
    window.addEventListener('online', handleOnline);
    window.addEventListener('offline', handleOffline);
    
    return () => {
      window.removeEventListener('online', handleOnline);
      window.removeEventListener('offline', handleOffline);
    };
  }, []);

  // Translations
  const translations = {
    en: {
      title: "Plant Disease Analyzer",
      subtitle: "AI-powered plant health detection",
      uploadImage: "Upload Image",
      takePhoto: "Take Photo",
      analyzing: "Analyzing...",
      offlineMode: "Offline Mode Active",
      onlineMode: "Online Mode",
      selectLanguage: "Select Language",
      results: "Analysis Results",
      plantName: "Plant Species",
      healthStatus: "Health Status",
      diseaseDetected: "Disease Detected",
      confidence: "Confidence",
      recommendations: "Recommendations",
      symptoms: "Symptoms",
      treatment: "Treatment",
      healthy: "Healthy",
      diseased: "Diseased",
      savedAnalyses: "Saved Analyses",
      noImage: "Please upload or capture an image first",
      downloadReport: "Download Report"
    },
    es: {
      title: "Analizador de Enfermedades de Plantas",
      subtitle: "Detección de salud vegetal con IA",
      uploadImage: "Subir Imagen",
      takePhoto: "Tomar Foto",
      analyzing: "Analizando...",
      offlineMode: "Modo Sin Conexión Activo",
      onlineMode: "Modo En Línea",
      selectLanguage: "Seleccionar Idioma",
      results: "Resultados del Análisis",
      plantName: "Especie de Planta",
      healthStatus: "Estado de Salud",
      diseaseDetected: "Enfermedad Detectada",
      confidence: "Confianza",
      recommendations: "Recomendaciones",
      symptoms: "Síntomas",
      treatment: "Tratamiento",
      healthy: "Saludable",
      diseased: "Enfermo",
      savedAnalyses: "Análisis Guardados",
      noImage: "Por favor sube o captura una imagen primero",
      downloadReport: "Descargar Informe"
    },
    hi: {
      title: "पौधों की बीमारी विश्लेषक",
      subtitle: "AI-संचालित पौधे स्वास्थ्य का पता लगाना",
      uploadImage: "छवि अपलोड करें",
      takePhoto: "फोटो लें",
      analyzing: "विश्लेषण कर रहे हैं...",
      offlineMode: "ऑफ़लाइन मोड सक्रिय",
      onlineMode: "ऑनलाइन मोड",
      selectLanguage: "भाषा चुनें",
      results: "विश्लेषण परिणाम",
      plantName: "पौधे की प्रजाति",
      healthStatus: "स्वास्थ्य स्थिति",
      diseaseDetected: "रोग का पता चला",
      confidence: "विश्वास",
      recommendations: "सिफारिशें",
      symptoms: "लक्षण",
      treatment: "उपचार",
      healthy: "स्वस्थ",
      diseased: "रोगग्रस्त",
      savedAnalyses: "सहेजे गए विश्लेषण",
      noImage: "कृपया पहले एक छवि अपलोड या कैप्चर करें",
      downloadReport: "रिपोर्ट डाउनलोड करें"
    },
    ta: {
      title: "தாவர நோய் பகுப்பாய்வி",
      subtitle: "AI-இயக்கப்படும் தாவர சுகாதார கண்டறிதல்",
      uploadImage: "படத்தை பதிவேற்றவும்",
      takePhoto: "புகைப்படம் எடுக்கவும்",
      analyzing: "பகுப்பாய்வு செய்கிறது...",
      offlineMode: "ஆஃப்லைன் பயன்முறை செயலில்",
      onlineMode: "ஆன்லைன் பயன்முறை",
      selectLanguage: "மொழியைத் தேர்ந்தெடுக்கவும்",
      results: "பகுப்பாய்வு முடிவுகள்",
      plantName: "தாவர இனம்",
      healthStatus: "சுகாதார நிலை",
      diseaseDetected: "நோய் கண்டறியப்பட்டது",
      confidence: "நம்பிக்கை",
      recommendations: "பரிந்துரைகள்",
      symptoms: "அறிகுறிகள்",
      treatment: "சிகிச்சை",
      healthy: "ஆரோக்கியமான",
      diseased: "நோயுற்ற",
      savedAnalyses: "சேமிக்கப்பட்ட பகுப்பாய்வுகள்",
      noImage: "முதலில் ஒரு படத்தை பதிவேற்றவும் அல்லது எடுக்கவும்",
      downloadReport: "அறிக்கையை பதிவிறக்கவும்"
    },
    fr: {
      title: "Analyseur de Maladies des Plantes",
      subtitle: "Détection de la santé des plantes par IA",
      uploadImage: "Télécharger l'Image",
      takePhoto: "Prendre une Photo",
      analyzing: "Analyse en cours...",
      offlineMode: "Mode Hors Ligne Actif",
      onlineMode: "Mode En Ligne",
      selectLanguage: "Sélectionner la Langue",
      results: "Résultats de l'Analyse",
      plantName: "Espèce de Plante",
      healthStatus: "État de Santé",
      diseaseDetected: "Maladie Détectée",
      confidence: "Confiance",
      recommendations: "Recommandations",
      symptoms: "Symptômes",
      treatment: "Traitement",
      healthy: "Sain",
      diseased: "Malade",
      savedAnalyses: "Analyses Sauvegardées",
      noImage: "Veuillez d'abord télécharger ou capturer une image",
      downloadReport: "Télécharger le Rapport"
    },
    zh: {
      title: "植物病害分析仪",
      subtitle: "AI驱动的植物健康检测",
      uploadImage: "上传图片",
      takePhoto: "拍照",
      analyzing: "分析中...",
      offlineMode: "离线模式已激活",
      onlineMode: "在线模式",
      selectLanguage: "选择语言",
      results: "分析结果",
      plantName: "植物物种",
      healthStatus: "健康状况",
      diseaseDetected: "检测到疾病",
      confidence: "置信度",
      recommendations: "建议",
      symptoms: "症状",
      treatment: "治疗",
      healthy: "健康",
      diseased: "患病",
      savedAnalyses: "已保存的分析",
      noImage: "请先上传或拍摄图片",
      downloadReport: "下载报告"
    }
  };

  const t = translations[language];

  // Simulated disease database for offline mode
  const diseaseDatabase = {
    tomato_blight: {
      en: { name: "Late Blight", symptoms: "Dark spots on leaves, white fungal growth", treatment: "Remove affected leaves, apply copper fungicide" },
      es: { name: "Tizón Tardío", symptoms: "Manchas oscuras en hojas, crecimiento fúngico blanco", treatment: "Eliminar hojas afectadas, aplicar fungicida de cobre" },
      hi: { name: "देर से झुलसा रोग", symptoms: "पत्तियों पर काले धब्बे, सफेद कवक वृद्धि", treatment: "प्रभावित पत्तियों को हटा दें, तांबा कवकनाशी लगाएं" },
      ta: { name: "தாமத வாடல்", symptoms: "இலைகளில் கரும்புள்ளிகள், வெள்ளை பூஞ்சை வளர்ச்சி", treatment: "பாதிக்கப்பட்ட இலைகளை அகற்றவும், செம்பு பூஞ்சைக்கொல்லி பயன்படுத்தவும்" },
      fr: { name: "Mildiou", symptoms: "Taches sombres sur les feuilles, croissance fongique blanche", treatment: "Retirer les feuilles affectées, appliquer un fongicide au cuivre" },
      zh: { name: "晚疫病", symptoms: "叶片上有黑斑，白色真菌生长", treatment: "移除受影响的叶子，施用铜杀菌剂" }
    },
    leaf_rust: {
      en: { name: "Leaf Rust", symptoms: "Orange-brown pustules on leaves", treatment: "Apply sulfur-based fungicide, improve air circulation" },
      es: { name: "Roya de la Hoja", symptoms: "Pústulas marrón-anaranjadas en hojas", treatment: "Aplicar fungicida a base de azufre, mejorar circulación de aire" },
      hi: { name: "पत्ती की जंग", symptoms: "पत्तियों पर नारंगी-भूरे रंग के दाने", treatment: "सल्फर-आधारित कवकनाशी लगाएं, वायु संचार में सुधार करें" },
      ta: { name: "இலை துரு", symptoms: "இலைகளில் ஆரஞ்சு-பழுப்பு கொப்புளங்கள்", treatment: "கந்தக அடிப்படையிலான பூஞ்சைக்கொல்லி பயன்படுத்தவும், காற்று சுழற்சியை மேம்படுத்தவும்" },
      fr: { name: "Rouille des Feuilles", symptoms: "Pustules orange-brun sur les feuilles", treatment: "Appliquer un fongicide à base de soufre, améliorer la circulation de l'air" },
      zh: { name: "叶锈病", symptoms: "叶片上有橙褐色脓疱", treatment: "施用硫基杀菌剂，改善空气流通" }
    }
  };

  const handleImageUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => {
        setImage(reader.result);
        setResult(null);
      };
      reader.readAsDataURL(file);
    }
  };

  const analyzeImage = () => {
    if (!image) {
      alert(t.noImage);
      return;
    }

    setAnalyzing(true);
    
    // Simulate AI analysis
    setTimeout(() => {
      const diseases = ['tomato_blight', 'leaf_rust', 'healthy'];
      const randomDisease = diseases[Math.floor(Math.random() * diseases.length)];
      const isHealthy = randomDisease === 'healthy';
      
      const analysisResult = {
        timestamp: new Date().toISOString(),
        plantSpecies: "Tomato (Solanum lycopersicum)",
        isHealthy: isHealthy,
        confidence: Math.floor(Math.random() * 15 + 85),
        disease: isHealthy ? null : diseaseDatabase[randomDisease][language],
        image: image
      };

      setResult(analysisResult);
      
      // Save to history
      setSavedAnalyses(prev => [analysisResult, ...prev].slice(0, 10));
      
      setAnalyzing(false);
    }, 2000);
  };

  const downloadReport = () => {
    if (!result) return;
    
    const report = `
Plant Disease Analysis Report
=============================
Date: ${new Date(result.timestamp).toLocaleString()}
Plant Species: ${result.plantSpecies}
Health Status: ${result.isHealthy ? t.healthy : t.diseased}
Confidence: ${result.confidence}%
${result.disease ? `
Disease: ${result.disease.name}
Symptoms: ${result.disease.symptoms}
Treatment: ${result.disease.treatment}
` : ''}
    `;
    
    const blob = new Blob([report], { type: 'text/plain' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = plant-analysis-${Date.now()}.txt;
    a.click();
    URL.revokeObjectURL(url);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-green-50 to-emerald-100 p-4">
      <div className="max-w-4xl mx-auto">
        {/* Header */}
        <div className="bg-white rounded-2xl shadow-lg p-6 mb-6">
          <div className="flex items-center justify-between mb-4">
            <div className="flex items-center gap-3">
              <div className="bg-green-500 p-3 rounded-xl">
                <Leaf className="w-8 h-8 text-white" />
              </div>
              <div>
                <h1 className="text-3xl font-bold text-gray-800">{t.title}</h1>
                <p className="text-gray-600">{t.subtitle}</p>
              </div>
            </div>
            <div className="flex items-center gap-2">
              {isOffline ? (
                <div className="flex items-center gap-2 px-3 py-2 bg-orange-100 text-orange-700 rounded-lg">
                  <WifiOff className="w-4 h-4" />
                  <span className="text-sm font-medium">{t.offlineMode}</span>
                </div>
              ) : (
                <div className="flex items-center gap-2 px-3 py-2 bg-green-100 text-green-700 rounded-lg">
                  <Wifi className="w-4 h-4" />
                  <span className="text-sm font-medium">{t.onlineMode}</span>
                </div>
              )}
            </div>
          </div>

          {/* Language Selector */}
          <div className="flex items-center gap-2">
            <Globe className="w-5 h-5 text-gray-600" />
            <select
              value={language}
              onChange={(e) => setLanguage(e.target.value)}
              className="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500"
            >
              <option value="en">English</option>
              <option value="es">Español</option>
              <option value="hi">हिन्दी</option>
              <option value="ta">தமிழ்</option>
              <option value="fr">Français</option>
              <option value="zh">中文</option>
            </select>
          </div>
        </div>

        {/* Upload Section */}
        <div className="bg-white rounded-2xl shadow-lg p-6 mb-6">
          <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
            <button
              onClick={() => fileInputRef.current.click()}
              className="flex items-center justify-center gap-3 px-6 py-4 bg-green-500 text-white rounded-xl hover:bg-green-600 transition-colors"
            >
              <Upload className="w-5 h-5" />
              <span className="font-medium">{t.uploadImage}</span>
            </button>
            <button
              onClick={() => cameraInputRef.current.click()}
              className="flex items-center justify-center gap-3 px-6 py-4 bg-blue-500 text-white rounded-xl hover:bg-blue-600 transition-colors"
            >
              <Camera className="w-5 h-5" />
              <span className="font-medium">{t.takePhoto}</span>
            </button>
          </div>

          <input
            ref={fileInputRef}
            type="file"
            accept="image/*"
            onChange={handleImageUpload}
            className="hidden"
          />
          <input
            ref={cameraInputRef}
            type="file"
            accept="image/*"
            capture="environment"
            onChange={handleImageUpload}
            className="hidden"
          />

          {image && (
            <div className="mb-4">
              <img
                src={image}
                alt="Plant"
                className="w-full h-64 object-cover rounded-xl"
              />
            </div>
          )}

          <button
            onClick={analyzeImage}
            disabled={!image || analyzing}
            className="w-full px-6 py-4 bg-emerald-600 text-white rounded-xl hover:bg-emerald-700 disabled:bg-gray-300 disabled:cursor-not-allowed transition-colors font-medium"
          >
            {analyzing ? t.analyzing : t.results}
          </button>
        </div>

        {/* Results Section */}
        {result && (
          <div className="bg-white rounded-2xl shadow-lg p-6 mb-6">
            <div className="flex items-center justify-between mb-4">
              <h2 className="text-2xl font-bold text-gray-800">{t.results}</h2>
              <button
                onClick={downloadReport}
                className="flex items-center gap-2 px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors"
              >
                <Download className="w-4 h-4" />
                {t.downloadReport}
              </button>
            </div>

            <div className="space-y-4">
              <div className="flex items-center gap-3 p-4 bg-gray-50 rounded-lg">
                <span className="font-semibold text-gray-700">{t.plantName}:</span>
                <span className="text-gray-600">{result.plantSpecies}</span>
              </div>

              <div className={`flex items-center gap-3 p-4 rounded-lg ${
                result.isHealthy ? 'bg-green-50' : 'bg-red-50'
              }`}>
                {result.isHealthy ? (
                  <CheckCircle className="w-6 h-6 text-green-600" />
                ) : (
                  <AlertCircle className="w-6 h-6 text-red-600" />
                )}
                <div className="flex-1">
                  <span className="font-semibold text-gray-700">{t.healthStatus}: </span>
                  <span className={result.isHealthy ? 'text-green-700' : 'text-red-700'}>
                    {result.isHealthy ? t.healthy : t.diseased}
                  </span>
                </div>
                <span className="text-sm text-gray-600">
                  {t.confidence}: {result.confidence}%
                </span>
              </div>

              {result.disease && (
                <>
                  <div className="p-4 bg-orange-50 rounded-lg">
                    <h3 className="font-semibold text-gray-800 mb-2">{t.diseaseDetected}</h3>
                    <p className="text-gray-700">{result.disease.name}</p>
                  </div>

                  <div className="p-4 bg-blue-50 rounded-lg">
                    <h3 className="font-semibold text-gray-800 mb-2">{t.symptoms}</h3>
                    <p className="text-gray-700">{result.disease.symptoms}</p>
                  </div>

                  <div className="p-4 bg-purple-50 rounded-lg">
                    <h3 className="font-semibold text-gray-800 mb-2">{t.treatment}</h3>
                    <p className="text-gray-700">{result.disease.treatment}</p>
                  </div>
                </>
              )}
            </div>
          </div>
        )}

        {/* Saved Analyses */}
        {savedAnalyses.length > 0 && (
          <div className="bg-white rounded-2xl shadow-lg p-6">
            <h2 className="text-2xl font-bold text-gray-800 mb-4">{t.savedAnalyses}</h2>
            <div className="space-y-3">
              {savedAnalyses.map((analysis, idx) => (
                <div
                  key={idx}
                  className="flex items-center gap-4 p-3 bg-gray-50 rounded-lg hover:bg-gray-100 transition-colors"
                >
                  <img
                    src={analysis.image}
                    alt="Saved analysis"
                    className="w-16 h-16 object-cover rounded-lg"
                  />
                  <div className="flex-1">
                    <p className="font-medium text-gray-800">
                      {analysis.isHealthy ? t.healthy : t.diseased}
                    </p>
                    <p className="text-sm text-gray-600">
                      {new Date(analysis.timestamp).toLocaleString()}
                    </p>
                  </div>
                  <span className={`px-3 py-1 rounded-full text-sm ${
                    analysis.isHealthy ? 'bg-green-100 text-green-700' : 'bg-red-100 text-red-700'
                  }`}>
                    {analysis.confidence}%
                  </span>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>
    </div>
  );
};

export default PlantDiseaseAnalyzer;

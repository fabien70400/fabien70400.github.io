import React, { useState, useEffect } from 'react';
import { Plus, Trash2, Edit3, Save, X, Calculator, Database, Download, FileText, Home } from 'lucide-react';

const RenovationPricingTool = () => {
  // Base de données des prix par défaut
  const [priceDatabase, setPriceDatabase] = useState({
    'Gros Oeuvre': {
      'Toiture': [
        { id: 1, name: 'Réfection couverture tuiles', unit: 'm²', price: 45 },
        { id: 2, name: 'Réfection couverture ardoises', unit: 'm²', price: 65 },
        { id: 3, name: 'Nettoyage toiture', unit: 'm²', price: 12 },
        { id: 4, name: 'Traitement antimousse', unit: 'm²', price: 8 },
        { id: 5, name: 'Remplacement gouttières', unit: 'ml', price: 35 },
        { id: 6, name: 'Installation velux', unit: 'u', price: 450 },
        { id: 7, name: 'Isolation toiture', unit: 'm²', price: 55 }
      ],
      'Charpente': [
        { id: 8, name: 'Traitement charpente', unit: 'm²', price: 25 },
        { id: 9, name: 'Remplacement poutre', unit: 'ml', price: 120 },
        { id: 10, name: 'Renforcement charpente', unit: 'm²', price: 35 },
        { id: 11, name: 'Traitement anti-insectes', unit: 'm²', price: 18 }
      ],
      'Maçonnerie': [
        { id: 12, name: 'Reprise fissures façade', unit: 'ml', price: 15 },
        { id: 13, name: 'Rejointoiement', unit: 'm²', price: 18 },
        { id: 14, name: 'Enduit façade', unit: 'm²', price: 25 },
        { id: 15, name: 'Ouverture mur porteur', unit: 'u', price: 1200 },
        { id: 16, name: 'Création ouverture fenêtre', unit: 'u', price: 850 },
        { id: 17, name: 'Reprise fondations', unit: 'ml', price: 180 }
      ],
      'Traitement EU': [
        { id: 18, name: 'Traitement humidité murs', unit: 'm²', price: 40 },
        { id: 19, name: 'Drainage périphérique', unit: 'ml', price: 85 },
        { id: 20, name: 'Injection résine', unit: 'ml', price: 35 },
        { id: 21, name: 'Cuvelage cave', unit: 'm²', price: 120 },
        { id: 22, name: 'Assèchement murs', unit: 'm²', price: 95 }
      ],
      'Menuiseries Extérieures': [
        { id: 23, name: 'Fenêtre PVC double vitrage', unit: 'u', price: 350 },
        { id: 24, name: 'Fenêtre alu double vitrage', unit: 'u', price: 480 },
        { id: 25, name: 'Porte-fenêtre PVC', unit: 'u', price: 650 },
        { id: 26, name: 'Porte d\'entrée blindée', unit: 'u', price: 1200 },
        { id: 27, name: 'Volets roulants électriques', unit: 'u', price: 420 },
        { id: 28, name: 'Volets battants bois', unit: 'u', price: 180 }
      ]
    },
    'Second Oeuvre': {
      'Cloisons': [
        { id: 29, name: 'Cloison BA13', unit: 'm²', price: 22 },
        { id: 30, name: 'Démontage cloison', unit: 'm²', price: 8 },
        { id: 31, name: 'Cloison hydrofuge', unit: 'm²', price: 28 },
        { id: 32, name: 'Cloison alvéolaire', unit: 'm²', price: 35 },
        { id: 33, name: 'Doublage mur BA13', unit: 'm²', price: 18 }
      ],
      'Isolation': [
        { id: 34, name: 'Isolation combles perdus', unit: 'm²', price: 15 },
        { id: 35, name: 'Isolation murs intérieurs', unit: 'm²', price: 35 },
        { id: 36, name: 'Isolation sol', unit: 'm²', price: 25 },
        { id: 37, name: 'Isolation phonique', unit: 'm²', price: 45 },
        { id: 38, name: 'Isolation thermique extérieure', unit: 'm²', price: 120 }
      ],
      'Plomberie': [
        { id: 39, name: 'Remplacement canalisation', unit: 'ml', price: 45 },
        { id: 40, name: 'Installation WC', unit: 'u', price: 180 },
        { id: 41, name: 'Installation lavabo', unit: 'u', price: 120 },
        { id: 42, name: 'Installation douche italienne', unit: 'u', price: 1200 },
        { id: 43, name: 'Installation baignoire', unit: 'u', price: 650 },
        { id: 44, name: 'Robinetterie haut de gamme', unit: 'u', price: 280 },
        { id: 45, name: 'Évacuation eaux usées', unit: 'ml', price: 55 }
      ],
      'Chauffage': [
        { id: 46, name: 'Radiateur électrique', unit: 'u', price: 150 },
        { id: 47, name: 'Chaudière gaz condensation', unit: 'u', price: 2500 },
        { id: 48, name: 'Plancher chauffant', unit: 'm²', price: 65 },
        { id: 49, name: 'Pompe à chaleur air/eau', unit: 'u', price: 8500 },
        { id: 50, name: 'Radiateur fonte design', unit: 'u', price: 320 },
        { id: 51, name: 'Cheminée insert', unit: 'u', price: 1800 }
      ],
      'Ventilation': [
        { id: 52, name: 'VMC simple flux', unit: 'u', price: 350 },
        { id: 53, name: 'VMC double flux', unit: 'u', price: 1200 },
        { id: 54, name: 'Extraction cuisine', unit: 'u', price: 85 },
        { id: 55, name: 'VMC hygroréglable', unit: 'u', price: 650 }
      ],
      'Électricité': [
        { id: 56, name: 'Réfection tableau électrique', unit: 'u', price: 450 },
        { id: 57, name: 'Point luminaire', unit: 'u', price: 35 },
        { id: 58, name: 'Prise électrique', unit: 'u', price: 25 },
        { id: 59, name: 'Interrupteur design', unit: 'u', price: 15 },
        { id: 60, name: 'Éclairage LED encastré', unit: 'u', price: 45 },
        { id: 61, name: 'Domotique installation de base', unit: 'u', price: 850 }
      ],
      'Menuiseries Intérieures': [
        { id: 62, name: 'Porte isoplane', unit: 'u', price: 120 },
        { id: 63, name: 'Porte postformée', unit: 'u', price: 180 },
        { id: 64, name: 'Porte coulissante', unit: 'u', price: 250 },
        { id: 65, name: 'Placard sur mesure', unit: 'ml', price: 180 },
        { id: 66, name: 'Escalier bois', unit: 'u', price: 2800 },
        { id: 67, name: 'Rampant escalier', unit: 'ml', price: 120 }
      ],
      'Revêtements Sols': [
        { id: 68, name: 'Carrelage sol standard', unit: 'm²', price: 35 },
        { id: 69, name: 'Carrelage sol haut de gamme', unit: 'm²', price: 65 },
        { id: 70, name: 'Parquet flottant', unit: 'm²', price: 28 },
        { id: 71, name: 'Parquet massif', unit: 'm²', price: 85 },
        { id: 72, name: 'Stratifié', unit: 'm²', price: 18 },
        { id: 73, name: 'Lino / PVC', unit: 'm²', price: 25 },
        { id: 74, name: 'Béton ciré', unit: 'm²', price: 120 },
        { id: 75, name: 'Moquette', unit: 'm²', price: 15 }
      ],
      'Revêtements Murs': [
        { id: 76, name: 'Peinture murs standard', unit: 'm²', price: 12 },
        { id: 77, name: 'Peinture haut de gamme', unit: 'm²', price: 22 },
        { id: 78, name: 'Papier peint pose', unit: 'm²', price: 18 },
        { id: 79, name: 'Carrelage mural', unit: 'm²', price: 45 },
        { id: 80, name: 'Lambris bois', unit: 'm²', price: 35 },
        { id: 81, name: 'Enduit décoratif', unit: 'm²', price: 28 }
      ]
    },
    'Forfaits & Prestations': {
      'Forfaits Électricité': [
        { id: 82, name: 'Rénovation électrique complète T2', unit: 'u', price: 3500 },
        { id: 83, name: 'Rénovation électrique complète T3', unit: 'u', price: 4800 },
        { id: 84, name: 'Rénovation électrique complète T4', unit: 'u', price: 6200 },
        { id: 85, name: 'Mise aux normes électriques', unit: 'u', price: 2200 },
        { id: 86, name: 'Installation domotique complète', unit: 'u', price: 3500 }
      ],
      'Forfaits Sanitaires': [
        { id: 87, name: 'Rénovation salle de bain complète 5m²', unit: 'u', price: 8500 },
        { id: 88, name: 'Rénovation salle de bain complète 8m²', unit: 'u', price: 12000 },
        { id: 89, name: 'WC suspendu avec bâti-support', unit: 'u', price: 650 },
        { id: 90, name: 'Douche à l\'italienne complète', unit: 'u', price: 2800 },
        { id: 91, name: 'Rénovation WC séparés', unit: 'u', price: 1800 }
      ],
      'Forfaits Cuisine': [
        { id: 92, name: 'Cuisine équipée entrée de gamme', unit: 'u', price: 4500 },
        { id: 93, name: 'Cuisine équipée milieu de gamme', unit: 'u', price: 8500 },
        { id: 94, name: 'Cuisine équipée haut de gamme', unit: 'u', price: 15000 },
        { id: 95, name: 'Îlot central avec plan de travail', unit: 'u', price: 2800 },
        { id: 96, name: 'Électroménager encastrable complet', unit: 'u', price: 3200 }
      ],
      'Prestations Diverses': [
        { id: 97, name: 'Nettoyage fin de chantier', unit: 'u', price: 350 },
        { id: 98, name: 'Évacuation gravats', unit: 'm³', price: 85 },
        { id: 99, name: 'Location benne 20m³', unit: 'u', price: 450 },
        { id: 100, name: 'Échafaudage facade', unit: 'm²', price: 12 },
        { id: 101, name: 'Protection chantier', unit: 'u', price: 280 },
        { id: 102, name: 'Diagnostic amiante/plomb', unit: 'u', price: 650 }
      ],
      'Aménagements Extérieurs': [
        { id: 103, name: 'Terrasse bois', unit: 'm²', price: 85 },
        { id: 104, name: 'Terrasse carrelée', unit: 'm²', price: 65 },
        { id: 105, name: 'Clôture grillage', unit: 'ml', price: 35 },
        { id: 106, name: 'Portail motorisé', unit: 'u', price: 1800 },
        { id: 107, name: 'Allée gravillonnée', unit: 'm²', price: 25 },
        { id: 108, name: 'Éclairage extérieur', unit: 'u', price: 180 }
      ]
    }
  });

  const [activeTab, setActiveTab] = useState('checklist');
  const [checklist, setChecklist] = useState({});
  const [editingPrice, setEditingPrice] = useState(null);
  const [newService, setNewService] = useState({ category: '', subcategory: '', name: '', unit: 'm²', price: '' });
  const [projectInfo, setProjectInfo] = useState({
    address: '',
    surface: '',
    salePrice: '',
    acquisitionPrice: '',
    description: ''
  });
  
  // Initialiser la checklist avec tous les services
  useEffect(() => {
    const initialChecklist = {};
    Object.keys(priceDatabase).forEach(category => {
      initialChecklist[category] = {};
      Object.keys(priceDatabase[category]).forEach(subcategory => {
        initialChecklist[category][subcategory] = {};
        priceDatabase[category][subcategory].forEach(service => {
          initialChecklist[category][subcategory][service.id] = {
            checked: false,
            quantity: 0,
            state: 'Bon'
          };
        });
      });
    });
    setChecklist(initialChecklist);
  }, [priceDatabase]);

  const updateChecklist = (category, subcategory, serviceId, field, value) => {
    setChecklist(prev => ({
      ...prev,
      [category]: {
        ...prev[category],
        [subcategory]: {
          ...prev[category][subcategory],
          [serviceId]: {
            ...prev[category][subcategory][serviceId],
            [field]: value
          }
        }
      }
    }));
  };

  const calculateTotal = () => {
    let total = 0;
    Object.keys(priceDatabase).forEach(category => {
      Object.keys(priceDatabase[category]).forEach(subcategory => {
        priceDatabase[category][subcategory].forEach(service => {
          const checklistItem = checklist[category]?.[subcategory]?.[service.id];
          if (checklistItem?.checked) {
            const multiplier = checklistItem.state === 'Mauvais' ? 1.5 : checklistItem.state === 'Moyen' ? 1.2 : 1;
            total += service.price * checklistItem.quantity * multiplier;
          }
        });
      });
    });
    return total;
  };

  const generatePDF = () => {
    // Créer et télécharger le PDF
    const printWindow = window.open('', '_blank');
    const pdfContent = `
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .header { background: #1e40af; color: white; padding: 20px; text-align: center; margin-bottom: 20px; }
        .project-info { background: #f8fafc; padding: 20px; margin-bottom: 20px; border-radius: 8px; }
        .financial-summary { background: #ecfdf5; padding: 20px; margin-bottom: 20px; border-radius: 8px; }
        .category { margin-bottom: 20px; }
        .category-header { background: #374151; color: white; padding: 10px; font-weight: bold; }
        .subcategory { margin-bottom: 15px; }
        .subcategory-header { background: #f1f5f9; padding: 8px; font-weight: bold; }
        table { width: 100%; border-collapse: collapse; margin-bottom: 15px; }
        th, td { border: 1px solid #e2e8f0; padding: 8px; text-align: left; }
        th { background: #f8fafc; font-weight: bold; }
        .total { background: #1e40af; color: white; padding: 15px; text-align: center; font-size: 18px; font-weight: bold; }
    </style>
</head>
<body>
    <div class="header">
        <h1>Estimation Travaux de Rénovation</h1>
        <p>Étude de faisabilité immobilière</p>
    </div>
    
    <div class="project-info">
        <h2>Informations du Projet</h2>
        <p><strong>Adresse:</strong> ${projectInfo.address || 'Non renseignée'}</p>
        <p><strong>Surface:</strong> ${projectInfo.surface || 'Non renseignée'} m²</p>
        <p><strong>Prix acquisition:</strong> ${parseFloat(projectInfo.acquisitionPrice || 0).toLocaleString('fr-FR')} €</p>
        <p><strong>Prix de vente visé:</strong> ${parseFloat(projectInfo.salePrice || 0).toLocaleString('fr-FR')} €</p>
        ${projectInfo.description ? `<p><strong>Description:</strong> ${projectInfo.description}</p>` : ''}
    </div>
    
    <div class="financial-summary">
        <h2>Récapitulatif Financier</h2>
        <p><strong>Coût des travaux:</strong> ${calculateTotal().toLocaleString('fr-FR')} €</p>
        <p><strong>Coût total:</strong> ${(parseFloat(projectInfo.acquisitionPrice || 0) + calculateTotal()).toLocaleString('fr-FR')} €</p>
        <p><strong>Marge potentielle:</strong> ${(parseFloat(projectInfo.salePrice || 0) - parseFloat(projectInfo.acquisitionPrice || 0) - calculateTotal()).toLocaleString('fr-FR')} €</p>
    </div>
    
    <div class="total">
        TOTAL ESTIMATION: ${calculateTotal().toLocaleString('fr-FR')} €
    </div>
    
    <div style="margin-top: 30px; text-align: center; color: #666;">
        Document généré le ${new Date().toLocaleDateString('fr-FR')} à ${new Date().toLocaleTimeString('fr-FR')}
    </div>
</body>
</html>`;

    printWindow.document.write(pdfContent);
    printWindow.document.close();
    
    setTimeout(() => {
      printWindow.focus();
      printWindow.print();
    }, 500);
  };

  const savePrice = (category, subcategory, serviceId) => {
    if (editingPrice) {
      setPriceDatabase(prev => ({
        ...prev,
        [category]: {
          ...prev[category],
          [subcategory]: prev[category][subcategory].map(service =>
            service.id === serviceId ? { ...service, ...editingPrice } : service
          )
        }
      }));
      setEditingPrice(null);
    }
  };

  const deleteService = (category, subcategory, serviceId) => {
    setPriceDatabase(prev => ({
      ...prev,
      [category]: {
        ...prev[category],
        [subcategory]: prev[category][subcategory].filter(service => service.id !== serviceId)
      }
    }));
  };

  const addNewService = () => {
    if (newService.name && newService.category && newService.subcategory && newService.price) {
      const maxId = Math.max(...Object.values(priceDatabase).flatMap(cat => 
        Object.values(cat).flatMap(subcat => subcat.map(service => service.id))
      ));
      
      const service = {
        id: maxId + 1,
        name: newService.name,
        unit: newService.unit,
        price: parseFloat(newService.price)
      };

      setPriceDatabase(prev => ({
        ...prev,
        [newService.category]: {
          ...prev[newService.category],
          [newService.subcategory]: [...prev[newService.category][newService.subcategory], service]
        }
      }));

      setNewService({ category: '', subcategory: '', name: '', unit: 'm²', price: '' });
    }
  };

  const renderChecklist = () => (
    <div className="space-y-6">
      {/* En-tête du projet */}
      <div className="bg-gradient-to-br from-slate-50 to-blue-50 p-6 rounded-xl border-2 border-blue-200 shadow-lg">
        <div className="flex items-center gap-3 mb-4">
          <Home className="w-6 h-6 text-blue-600" />
          <h3 className="text-xl font-bold text-slate-900">Informations du Projet</h3>
        </div>
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          <div className="space-y-2">
            <label className="flex items-center gap-2 text-sm font-medium text-gray-700">
              <Home className="w-4 h-4" />
              Adresse
            </label>
            <input
              type="text"
              value={projectInfo.address}
              onChange={(e) => setProjectInfo({...projectInfo, address: e.target.value})}
              className="w-full p-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all"
              placeholder="Adresse du bien"
            />
          </div>
          <div className="space-y-2">
            <label className="text-sm font-medium text-gray-700">Surface (m²)</label>
            <input
              type="number"
              value={projectInfo.surface}
              onChange={(e) => setProjectInfo({...projectInfo, surface: e.target.value})}
              className="w-full p-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all"
              placeholder="Surface habitable"
            />
          </div>
          <div className="space-y-2">
            <label className="text-sm font-medium text-gray-700">Prix de vente (€)</label>
            <input
              type="number"
              value={projectInfo.salePrice}
              onChange={(e) => setProjectInfo({...projectInfo, salePrice: e.target.value})}
              className="w-full p-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all"
              placeholder="Prix de vente visé"
            />
          </div>
          <div className="space-y-2">
            <label className="text-sm font-medium text-gray-700">Prix d'acquisition (€)</label>
            <input
              type="number"
              value={projectInfo.acquisitionPrice}
              onChange={(e) => setProjectInfo({...projectInfo, acquisitionPrice: e.target.value})}
              className="w-full p-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all"
              placeholder="Prix d'achat"
            />
          </div>
          <div className="md:col-span-2 space-y-2">
            <label className="text-sm font-medium text-gray-700">Description</label>
            <textarea
              value={projectInfo.description}
              onChange={(e) => setProjectInfo({...projectInfo, description: e.target.value})}
              className="w-full p-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all resize-none"
              placeholder="Notes sur le bien..."
              rows="3"
            />
          </div>
        </div>
      </div>

      {/* Récapitulatif financier */}
      <div className="bg-gradient-to-br from-blue-50 to-indigo-100 p-6 rounded-xl border-2 border-blue-300 shadow-lg">
        <div className="flex items-center justify-between mb-4">
          <div className="flex items-center gap-3">
            <Calculator className="w-6 h-6 text-blue-600" />
            <h3 className="text-xl font-bold text-blue-900">Récapitulatif Financier</h3>
          </div>
          <button
            onClick={generatePDF}
            className="flex items-center gap-2 bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg font-medium transition-all transform hover:scale-105 shadow-md"
          >
            <Download className="w-4 h-4" />
            Exporter PDF
          </button>
        </div>
        <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
          <div className="bg-white p-4 rounded-lg shadow-md border-l-4 border-blue-500">
            <p className="text-sm text-gray-600 mb-1">Coût des travaux</p>
            <p className="text-2xl font-bold text-blue-700">{calculateTotal().toLocaleString('fr-FR')} €</p>
          </div>
          <div className="bg-white p-4 rounded-lg shadow-md border-l-4 border-purple-500">
            <p className="text-sm text-gray-600 mb-1">Prix d'acquisition</p>
            <p className="text-xl font-semibold text-gray-800">{parseFloat(projectInfo.acquisitionPrice || 0).toLocaleString('fr-FR')} €</p>
          </div>
          <div className="bg-white p-4 rounded-lg shadow-md border-l-4 border-orange-500">
            <p className="text-sm text-gray-600 mb-1">Coût total</p>
            <p className="text-xl font-semibold text-gray-800">
              {(parseFloat(projectInfo.acquisitionPrice || 0) + calculateTotal()).toLocaleString('fr-FR')} €
            </p>
          </div>
          <div className="bg-white p-4 rounded-lg shadow-md border-l-4 border-green-500">
            <p className="text-sm text-gray-600 mb-1">Marge potentielle</p>
            <p className={`text-xl font-bold ${
              parseFloat(projectInfo.salePrice || 0) - parseFloat(projectInfo.acquisitionPrice || 0) - calculateTotal() > 0 
                ? 'text-green-600' : 'text-red-600'
            }`}>
              {(parseFloat(projectInfo.salePrice || 0) - parseFloat(projectInfo.acquisitionPrice || 0) - calculateTotal()).toLocaleString('fr-FR')} €
            </p>
          </div>
        </div>
      </div>

      {/* Check-list des travaux */}
      {Object.keys(priceDatabase).map(category => (
        <div key={category} className="border-2 border-gray-200 rounded-xl shadow-lg overflow-hidden">
          <h2 className="bg-gradient-to-r from-gray-700 to-gray-600 text-white p-4 font-bold text-lg flex items-center gap-2">
            <FileText className="w-5 h-5" />
            {category}
          </h2>
          
          {Object.keys(priceDatabase[category]).map(subcategory => (
            <div key={subcategory} className="border-t-2 border-gray-200">
              <h3 className="bg-gradient-to-r from-gray-50 to-blue-50 p-3 font-semibold text-md border-l-4 border-blue-500">{subcategory}</h3>
              
              {/* En-têtes de colonnes */}
              <div className="p-3 bg-gradient-to-r from-gray-100 to-gray-50 grid grid-cols-12 gap-2 text-xs font-bold text-gray-700 border-t border-gray-200">
                <div className="col-span-1">✓</div>
                <div className="col-span-4">Prestation</div>
                <div className="col-span-2">Quantité</div>
                <div className="col-span-1">Unité</div>
                <div className="col-span-1">P.U.</div>
                <div className="col-span-2">État</div>
                <div className="col-span-1">Total</div>
              </div>
              
              {priceDatabase[category][subcategory].map(service => {
                const checklistItem = checklist[category]?.[subcategory]?.[service.id] || {};
                return (
                  <div key={service.id} className="p-3 border-t border-gray-100 grid grid-cols-12 gap-2 items-center hover:bg-blue-25 transition-colors">
                    <div className="col-span-1">
                      <input
                        type="checkbox"
                        checked={checklistItem.checked || false}
                        onChange={(e) => updateChecklist(category, subcategory, service.id, 'checked', e.target.checked)}
                        className="w-5 h-5 text-blue-600 rounded focus:ring-2 focus:ring-blue-500"
                      />
                    </div>
                    
                    <div className="col-span-4 text-sm font-medium text-gray-800">{service.name}</div>
                    
                    <div className="col-span-2">
                      <input
                        type="number"
                        min="0"
                        step="0.1"
                        value={checklistItem.quantity || 0}
                        onChange={(e) => updateChecklist(category, subcategory, service.id, 'quantity', parseFloat(e.target.value) || 0)}
                        className="w-full p-2 border-2 border-gray-200 rounded-lg text-sm focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all disabled:bg-gray-100"
                        disabled={!checklistItem.checked}
                      />
                    </div>
                    
                    <div className="col-span-1 text-sm text-gray-600 text-center font-medium">{service.unit}</div>
                    
                    <div className="col-span-1 text-sm text-gray-700 text-center font-bold">{service.price} €</div>
                    
                    <div className="col-span-2">
                      <select
                        value={checklistItem.state || 'Bon'}
                        onChange={(e) => updateChecklist(category, subcategory, service.id, 'state', e.target.value)}
                        className="w-full p-2 border-2 border-gray-200 rounded-lg text-sm focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all disabled:bg-gray-100"
                        disabled={!checklistItem.checked}
                      >
                        <option value="Bon">Bon</option>
                        <option value="Moyen">Moyen (+20%)</option>
                        <option value="Mauvais">Mauvais (+50%)</option>
                      </select>
                    </div>
                    
                    <div className="col-span-1 text-right">
                      {checklistItem.checked && (
                        <span className="inline-block bg-gradient-to-r from-green-500 to-green-600 text-white px-2 py-1 rounded-lg font-bold text-sm shadow-md">
                          {(service.price * (checklistItem.quantity || 0) * 
                            (checklistItem.state === 'Mauvais' ? 1.5 : checklistItem.state === 'Moyen' ? 1.2 : 1)
                          ).toLocaleString('fr-FR')} €
                        </span>
                      )}
                    </div>
                  </div>
                );
              })}
            </div>
          ))}
        </div>
      ))}
    </div>
  );

  const renderPriceDatabase = () => (
    <div className="space-y-6">
      <div className="bg-gradient-to-br from-green-50 to-emerald-100 p-6 rounded-xl border-2 border-green-300 shadow-lg">
        <div className="flex items-center gap-3 mb-4">
          <Database className="w-6 h-6 text-green-600" />
          <h3 className="text-xl font-bold text-green-900">Ajouter une Prestation</h3>
        </div>
        
        <div className="grid grid-cols-2 md:grid-cols-5 gap-3">
          <select
            value={newService.category}
            onChange={(e) => setNewService({...newService, category: e.target.value, subcategory: ''})}
            className="p-3 border-2 border-gray-200 rounded-lg focus:border-green-500 focus:ring-2 focus:ring-green-200 transition-all"
          >
            <option value="">Catégorie</option>
            {Object.keys(priceDatabase).map(cat => (
              <option key={cat} value={cat}>{cat}</option>
            ))}
          </select>
          
          <select
            value={newService.subcategory}
            onChange={(e) => setNewService({...newService, subcategory: e.target.value})}
            className="p-3 border-2 border-gray-200 rounded-lg focus:border-green-500 focus:ring-2 focus:ring-green-200 transition-all disabled:bg-gray-100"
            disabled={!newService.category}
          >
            <option value="">Sous-catégorie</option>
            {newService.category && Object.keys(priceDatabase[newService.category]).map(subcat => (
              <option key={subcat} value={subcat}>{subcat}</option>
            ))}
          </select>
          
          <input
            type="text"
            placeholder="Nom de la prestation"
            value={newService.name}
            onChange={(e) => setNewService({...newService, name: e.target.value})}
            className="p-3 border-2 border-gray-200 rounded-lg focus:border-green-500 focus:ring-2 focus:ring-green-200 transition-all"
          />
          
          <div className="flex gap-1">
            <input
              type="number"
              placeholder="Prix"
              value={newService.price}
              onChange={(e) => setNewService({...newService, price: e.target.value})}
              className="flex-1 p-3 border-2 border-gray-200 rounded-lg focus:border-green-500 focus:ring-2 focus:ring-green-200 transition-all"
            />
            <select
              value={newService.unit}
              onChange={(e) => setNewService({...newService, unit: e.target.value})}
              className="p-3 border-2 border-gray-200 rounded-lg focus:border-green-500 focus:ring-2 focus:ring-green-200 transition-all"
            >
              <option value="m²">m²</option>
              <option value="ml">ml</option>
              <option value="u">u</option>
              <option value="m³">m³</option>
            </select>
          </div>
          
          <button
            onClick={addNewService}
            className="flex items-center justify-center gap-2 bg-gradient-to-r from-green-600 to-green-700 text-white p-3 rounded-lg hover:from-green-700 hover:to-green-800 font-bold transition-all transform hover:scale-105 shadow-md"
          >
            <Plus className="w-5 h-5" />
            Ajouter
          </button>
        </div>
      </div>

      {Object.keys(priceDatabase).map(category => (
        <div key={category} className="border-2 border-gray-200 rounded-xl shadow-lg overflow-hidden">
          <h2 className="bg-gradient-to-r from-gray-700 to-gray-600 text-white p-4 font-bold text-lg flex items-center gap-2">
            <FileText className="w-5 h-5" />
            {category}
          </h2>
          
          {Object.keys(priceDatabase[category]).map(subcategory => (
            <div key={subcategory} className="border-t-2 border-gray-200">
              <h3 className="bg-gradient-to-r from-gray-50 to-blue-50 p-3 font-semibold border-l-4 border-blue-500">{subcategory}</h3>
              
              <div className="grid grid-cols-12 gap-2 p-3 bg-gradient-to-r from-gray-100 to-gray-50 text-sm font-bold text-gray-700">
                <div className="col-span-5">Prestation</div>
                <div className="col-span-2">Prix</div>
                <div className="col-span-2">Unité</div>
                <div className="col-span-3 text-center">Actions</div>
              </div>
              
              {priceDatabase[category][subcategory].map(service => (
                <div key={service.id} className="grid grid-cols-12 gap-2 p-3 border-t border-gray-100 items-center hover:bg-blue-25 transition-colors">
                  <div className="col-span-5">
                    {editingPrice && editingPrice.id === service.id ? (
                      <input
                        type="text"
                        value={editingPrice.name}
                        onChange={(e) => setEditingPrice({...editingPrice, name: e.target.value})}
                        className="w-full p-2 border-2 border-blue-300 rounded-lg focus:border-blue-500 focus:ring-2 focus:ring-blue-200"
                      />
                    ) : (
                      <span className="text-sm font-medium text-gray-800">{service.name}</span>
                    )}
                  </div>
                  
                  <div className="col-span-2">
                    {editingPrice && editingPrice.id === service.id ? (
                      <input
                        type="number"
                        value={editingPrice.price}
                        onChange={(e) => setEditingPrice({...editingPrice, price: parseFloat(e.target.value)})}
                        className="w-full p-2 border-2 border-blue-300 rounded-lg focus:border-blue-500 focus:ring-2 focus:ring-blue-200"
                      />
                    ) : (
                      <span className="text-sm font-bold text-green-600">{service.price} €</span>
                    )}
                  </div>
                  
                  <div className="col-span-2">
                    {editingPrice && editingPrice.id === service.id ? (
                      <select
                        value={editingPrice.unit}
                        onChange={(e) => setEditingPrice({...editingPrice, unit: e.target.value})}
                        className="w-full p-2 border-2 border-blue-300 rounded-lg focus:border-blue-500 focus:ring-2 focus:ring-blue-200"
                      >
                        <option value="m²">m²</option>
                        <option value="ml">ml</option>
                        <option value="u">u</option>
                        <option value="m³">m³</option>
                      </select>
                    ) : (
                      <span className="text-sm text-gray-600 font-medium">{service.unit}</span>
                    )}
                  </div>
                  
                  <div className="col-span-3 flex justify-center gap-2">
                    {editingPrice && editingPrice.id === service.id ? (
                      <>
                        <button
                          onClick={() => savePrice(category, subcategory, service.id)}
                          className="p-2 text-green-600 hover:bg-green-100 rounded-lg transition-colors"
                        >
                          <Save className="w-4 h-4" />
                        </button>
                        <button
                          onClick={() => setEditingPrice(null)}
                          className="p-2 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors"
                        >
                          <X className="w-4 h-4" />
                        </button>
                      </>
                    ) : (
                      <>
                        <button
                          onClick={() => setEditingPrice({...service})}
                          className="p-2 text-blue-600 hover:bg-blue-100 rounded-lg transition-colors"
                        >
                          <Edit3 className="w-4 h-4" />
                        </button>
                        <button
                          onClick={() => deleteService(category, subcategory, service.id)}
                          className="p-2 text-red-600 hover:bg-red-100 rounded-lg transition-colors"
                        >
                          <Trash2 className="w-4 h-4" />
                        </button>
                      </>
                    )}
                  </div>
                </div>
              ))}
            </div>
          ))}
        </div>
      ))}
    </div>
  );

  return (
    <div className="max-w-7xl mx-auto p-4 bg-gradient-to-br from-gray-50 to-blue-50 min-h-screen">
      <div className="mb-8">
        <div className="text-center bg-white p-6 rounded-2xl shadow-xl border-2 border-blue-200">
          <h1 className="text-4xl font-bold bg-gradient-to-r from-blue-600 to-indigo-600 bg-clip-text text-transparent mb-2">
            Chiffrage Travaux Immobiliers
          </h1>
          <p className="text-gray-600 text-lg">Interface professionnelle de chiffrage pour prospection immobilière</p>
        </div>
      </div>

      <div className="mb-6">
        <div className="bg-white rounded-xl shadow-lg border-2 border-gray-200 overflow-hidden">
          <nav className="flex">
            <button
              onClick={() => setActiveTab('checklist')}
              className={`flex-1 py-4 px-6 font-bold text-lg transition-all ${
                activeTab === 'checklist'
                  ? 'bg-gradient-to-r from-blue-500 to-blue-600 text-white shadow-lg'
                  : 'text-gray-600 hover:text-blue-600 hover:bg-blue-50'
              }`}
            >
              Check-list & Chiffrage
            </button>
            <button
              onClick={() => setActiveTab('database')}
              className={`flex-1 py-4 px-6 font-bold text-lg transition-all ${
                activeTab === 'database'
                  ? 'bg-gradient-to-r from-blue-500 to-blue-600 text-white shadow-lg'
                  : 'text-gray-600 hover:text-blue-600 hover:bg-blue-50'
              }`}
            >
              Base de Données Prix
            </button>
          </nav>
        </div>
      </div>

      <div className="bg-white rounded-xl shadow-lg p-6">
        {activeTab === 'checklist' && renderChecklist()}
        {activeTab === 'database' && renderPriceDatabase()}
      </div>
    </div>
  );
};

export default RenovationPricingTool;

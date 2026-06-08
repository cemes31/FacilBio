<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FacilBio – Gestion Agriculture Biologique</title>
<script src="https://unpkg.com/react@18/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --vert-fonce: #1a3a2a;
    --vert-moyen: #2d5a3d;
    --vert-clair: #4a8c5c;
    --vert-doux: #7db88a;
    --vert-pale: #c8e6c9;
    --terre: #8b5e3c;
    --terre-clair: #c49a6c;
    --creme: #f7f3ee;
    --blanc: #ffffff;
    --or: #d4a843;
    --rouge-bio: #c0392b;
    --gris-texte: #3d3d3d;
    --gris-clair: #e8e4df;
    --ombre: 0 4px 24px rgba(26,58,42,0.12);
    --ombre-forte: 0 8px 40px rgba(26,58,42,0.2);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--creme);
    color: var(--gris-texte);
    min-height: 100vh;
  }

  /* SIDEBAR */
  .sidebar {
    position: fixed;
    left: 0; top: 0;
    width: 240px;
    height: 100vh;
    background: var(--vert-fonce);
    display: flex;
    flex-direction: column;
    z-index: 100;
    box-shadow: var(--ombre-forte);
  }

  .logo-zone {
    padding: 28px 24px 24px;
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }

  .logo-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    color: var(--blanc);
    letter-spacing: -0.5px;
    line-height: 1;
  }

  .logo-title span { color: var(--vert-doux); }

  .logo-sub {
    font-size: 0.7rem;
    color: var(--vert-pale);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-top: 4px;
    opacity: 0.7;
  }

  .label-ab {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background: var(--or);
    color: var(--vert-fonce);
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    padding: 3px 8px;
    border-radius: 20px;
    margin-top: 10px;
  }

  .nav-section {
    padding: 16px 0;
    flex: 1;
    overflow-y: auto;
  }

  .nav-label {
    font-size: 0.6rem;
    letter-spacing: 2.5px;
    text-transform: uppercase;
    color: var(--vert-doux);
    padding: 8px 24px 4px;
    opacity: 0.8;
  }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 11px 24px;
    cursor: pointer;
    color: rgba(255,255,255,0.65);
    font-size: 0.875rem;
    font-weight: 400;
    transition: all 0.2s;
    border-left: 3px solid transparent;
    position: relative;
  }

  .nav-item:hover {
    color: var(--blanc);
    background: rgba(255,255,255,0.06);
  }

  .nav-item.active {
    color: var(--blanc);
    background: rgba(125,184,138,0.15);
    border-left-color: var(--vert-doux);
    font-weight: 500;
  }

  .nav-icon { font-size: 1.1rem; width: 20px; text-align: center; }

  .nav-badge {
    margin-left: auto;
    background: var(--or);
    color: var(--vert-fonce);
    font-size: 0.6rem;
    font-weight: 700;
    padding: 2px 6px;
    border-radius: 10px;
  }

  .sidebar-bottom {
    padding: 16px 24px;
    border-top: 1px solid rgba(255,255,255,0.1);
    font-size: 0.75rem;
    color: rgba(255,255,255,0.35);
  }

  /* MAIN */
  .main {
    margin-left: 240px;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  .topbar {
    background: var(--blanc);
    border-bottom: 1px solid var(--gris-clair);
    padding: 16px 32px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: sticky;
    top: 0;
    z-index: 50;
  }

  .page-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.4rem;
    color: var(--vert-fonce);
    font-weight: 600;
  }

  .topbar-right {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 9px 18px;
    border-radius: 8px;
    font-size: 0.875rem;
    font-weight: 500;
    cursor: pointer;
    border: none;
    transition: all 0.2s;
    font-family: 'DM Sans', sans-serif;
  }

  .btn-primary {
    background: var(--vert-moyen);
    color: var(--blanc);
  }
  .btn-primary:hover { background: var(--vert-fonce); }

  .btn-outline {
    background: transparent;
    color: var(--vert-moyen);
    border: 1.5px solid var(--vert-moyen);
  }
  .btn-outline:hover { background: var(--vert-pale); }

  .btn-danger {
    background: #fee2e2;
    color: var(--rouge-bio);
    border: none;
  }
  .btn-danger:hover { background: #fecaca; }

  .btn-sm { padding: 6px 12px; font-size: 0.8rem; }

  .content {
    padding: 28px 32px;
    flex: 1;
  }

  /* CARDS */
  .card {
    background: var(--blanc);
    border-radius: 12px;
    box-shadow: var(--ombre);
    overflow: hidden;
  }

  .card-header {
    padding: 18px 24px;
    border-bottom: 1px solid var(--gris-clair);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .card-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.05rem;
    color: var(--vert-fonce);
    font-weight: 600;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .card-body { padding: 20px 24px; }

  /* DASHBOARD */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    margin-bottom: 24px;
  }

  .stat-card {
    background: var(--blanc);
    border-radius: 12px;
    padding: 20px;
    box-shadow: var(--ombre);
    border-top: 4px solid var(--vert-clair);
    position: relative;
    overflow: hidden;
  }

  .stat-card::after {
    content: '';
    position: absolute;
    bottom: -20px; right: -20px;
    width: 80px; height: 80px;
    background: var(--vert-pale);
    border-radius: 50%;
    opacity: 0.3;
  }

  .stat-card.orange { border-top-color: var(--or); }
  .stat-card.terre { border-top-color: var(--terre-clair); }
  .stat-card.alert { border-top-color: var(--rouge-bio); }

  .stat-emoji { font-size: 1.5rem; margin-bottom: 8px; }
  .stat-val {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    color: var(--vert-fonce);
    line-height: 1;
    font-weight: 700;
  }
  .stat-label { font-size: 0.8rem; color: #666; margin-top: 4px; }
  .stat-sub { font-size: 0.72rem; color: var(--vert-clair); margin-top: 6px; font-weight: 500; }

  .dash-grid {
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 20px;
    margin-bottom: 20px;
  }

  /* ALERTES */
  .alert-item {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 12px 0;
    border-bottom: 1px solid var(--gris-clair);
  }
  .alert-item:last-child { border-bottom: none; padding-bottom: 0; }
  .alert-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    margin-top: 5px;
    flex-shrink: 0;
  }
  .alert-dot.rouge { background: var(--rouge-bio); }
  .alert-dot.orange { background: var(--or); }
  .alert-dot.vert { background: var(--vert-clair); }
  .alert-text { font-size: 0.85rem; line-height: 1.4; }
  .alert-date { font-size: 0.72rem; color: #999; margin-top: 2px; }

  /* TABLEAU */
  table { width: 100%; border-collapse: collapse; }
  th {
    background: var(--creme);
    padding: 10px 16px;
    text-align: left;
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.5px;
    color: #666;
    text-transform: uppercase;
  }
  td {
    padding: 12px 16px;
    font-size: 0.875rem;
    border-bottom: 1px solid var(--gris-clair);
    vertical-align: middle;
  }
  tr:last-child td { border-bottom: none; }
  tr:hover td { background: #fafaf8; }

  /* BADGES */
  .badge {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    padding: 3px 10px;
    border-radius: 20px;
    font-size: 0.72rem;
    font-weight: 600;
    letter-spacing: 0.3px;
  }
  .badge-ab { background: #e8f5e9; color: #2e7d32; }
  .badge-conv { background: #fff8e1; color: #f57f17; }
  .badge-ok { background: #e3f2fd; color: #1565c0; }
  .badge-alert { background: #ffebee; color: #c62828; }
  .badge-neutre { background: var(--gris-clair); color: #555; }

  /* FORMULAIRE */
  .form-grid { display: grid; gap: 16px; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .form-row-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }
  .form-group { display: flex; flex-direction: column; gap: 6px; }
  label { font-size: 0.8rem; font-weight: 600; color: var(--vert-fonce); }

  input, select, textarea {
    padding: 9px 13px;
    border: 1.5px solid var(--gris-clair);
    border-radius: 8px;
    font-size: 0.875rem;
    font-family: 'DM Sans', sans-serif;
    color: var(--gris-texte);
    background: var(--blanc);
    transition: border-color 0.2s;
  }
  input:focus, select:focus, textarea:focus {
    outline: none;
    border-color: var(--vert-clair);
  }
  textarea { resize: vertical; min-height: 80px; }

  /* MODALE */
  .modal-overlay {
    position: fixed; inset: 0;
    background: rgba(26,58,42,0.5);
    backdrop-filter: blur(4px);
    z-index: 200;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 24px;
  }
  .modal {
    background: var(--blanc);
    border-radius: 16px;
    box-shadow: var(--ombre-forte);
    width: 100%;
    max-width: 580px;
    max-height: 85vh;
    overflow-y: auto;
  }
  .modal-header {
    padding: 20px 24px 16px;
    border-bottom: 1px solid var(--gris-clair);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .modal-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.1rem;
    color: var(--vert-fonce);
  }
  .modal-close {
    background: none; border: none;
    font-size: 1.4rem; cursor: pointer;
    color: #999; line-height: 1;
  }
  .modal-body { padding: 20px 24px; }
  .modal-footer {
    padding: 16px 24px;
    border-top: 1px solid var(--gris-clair);
    display: flex;
    gap: 10px;
    justify-content: flex-end;
  }

  /* CONVERSION PROGRESS */
  .conv-bar-wrap {
    background: var(--gris-clair);
    border-radius: 20px;
    height: 10px;
    overflow: hidden;
    margin: 6px 0;
  }
  .conv-bar {
    height: 100%;
    background: linear-gradient(90deg, var(--vert-clair), var(--vert-doux));
    border-radius: 20px;
    transition: width 0.6s ease;
  }

  /* PRODUITS PHYTO AB */
  .produit-item {
    padding: 12px 16px;
    border: 1.5px solid var(--gris-clair);
    border-radius: 10px;
    display: flex;
    align-items: center;
    gap: 12px;
    cursor: pointer;
    transition: all 0.2s;
  }
  .produit-item:hover { border-color: var(--vert-clair); background: #f0f7f1; }
  .produit-info { flex: 1; }
  .produit-nom { font-size: 0.9rem; font-weight: 600; color: var(--vert-fonce); }
  .produit-substance { font-size: 0.75rem; color: #777; }
  .produit-ab { font-size: 1.2rem; }

  .search-box {
    position: relative;
    margin-bottom: 16px;
  }
  .search-box input { padding-left: 36px; width: 100%; }
  .search-icon {
    position: absolute;
    left: 12px; top: 50%;
    transform: translateY(-50%);
    color: #999;
    font-size: 0.9rem;
  }

  /* CERTIF */
  .certif-card {
    border: 2px solid var(--vert-pale);
    border-radius: 12px;
    padding: 20px;
    position: relative;
    overflow: hidden;
  }
  .certif-card::before {
    content: '🌿';
    position: absolute;
    right: 16px; top: 16px;
    font-size: 2rem;
    opacity: 0.15;
  }
  .certif-org { font-size: 0.75rem; color: #888; text-transform: uppercase; letter-spacing: 1px; }
  .certif-num { font-family: 'Playfair Display', serif; font-size: 1.2rem; color: var(--vert-fonce); margin: 4px 0; }
  .certif-info { font-size: 0.85rem; color: #555; }

  /* EMPTY */
  .empty-state {
    text-align: center;
    padding: 40px 20px;
    color: #999;
  }
  .empty-icon { font-size: 2.5rem; margin-bottom: 12px; }
  .empty-text { font-size: 0.9rem; }

  /* TABS */
  .tabs {
    display: flex;
    gap: 4px;
    background: var(--gris-clair);
    padding: 4px;
    border-radius: 10px;
    margin-bottom: 20px;
  }
  .tab {
    flex: 1;
    padding: 8px 16px;
    border-radius: 7px;
    cursor: pointer;
    font-size: 0.85rem;
    font-weight: 500;
    text-align: center;
    color: #666;
    transition: all 0.2s;
    border: none;
    background: none;
    font-family: 'DM Sans', sans-serif;
  }
  .tab.active {
    background: var(--blanc);
    color: var(--vert-fonce);
    box-shadow: var(--ombre);
  }

  /* INFO BOX */
  .info-box {
    background: linear-gradient(135deg, #e8f5e9, #f1f8e9);
    border: 1.5px solid var(--vert-pale);
    border-radius: 10px;
    padding: 14px 18px;
    font-size: 0.83rem;
    color: var(--vert-fonce);
    line-height: 1.6;
    margin-bottom: 16px;
  }
  .info-box strong { font-weight: 600; }

  /* FERTILISANT */
  .fertil-badge {
    padding: 2px 8px;
    border-radius: 12px;
    font-size: 0.7rem;
    font-weight: 600;
  }
  .fertil-autorise { background: #e8f5e9; color: #2e7d32; }
  .fertil-conditionnel { background: #fff8e1; color: #e65100; }

  .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
  .grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }
</style>
</head>
<body>
<div id="root"></div>

<script type="text/babel">
const { useState } = React;

// ===================== DONNÉES DEMO =====================
const PARCELLES_INIT = [
  { id: 1, nom: "Le Pré Long", surface: 4.2, culture: "Blé tendre", statut: "certifie", debut_conversion: "2021-01-15", organisme: "Ecocert" },
  { id: 2, nom: "La Côte Sud", surface: 2.8, culture: "Maraîchage", statut: "certifie", debut_conversion: "2020-06-01", organisme: "Ecocert" },
  { id: 3, nom: "Champ du Moulin", surface: 6.5, culture: "Tournesol", statut: "conversion", debut_conversion: "2024-03-10", organisme: "Bureau Veritas" },
  { id: 4, nom: "Les Terrasses", surface: 1.9, culture: "Vigne", statut: "conversion", debut_conversion: "2023-11-01", organisme: "Certipaq" },
];

const INTRANTS_AB = [
  { id: 1, nom: "Bouillie bordelaise", substance: "Sulfate de cuivre", categorie: "Fongicide", usages: "Mildiou vigne, tomate", amm: "2120058" },
  { id: 2, nom: "Soufre mouillable", substance: "Soufre", categorie: "Fongicide / Acaricide", usages: "Oïdium, acariens", amm: "9900282" },
  { id: 3, nom: "Pyrèthre naturel", substance: "Pyréthrine naturelle", categorie: "Insecticide", usages: "Pucerons, thrips", amm: "8900276" },
  { id: 4, nom: "Spinosad", substance: "Spinosad", categorie: "Insecticide", usages: "Mouche cerise, chenilles", amm: "2100156" },
  { id: 5, nom: "Huile essentielle d'orange", substance: "Limonène", categorie: "Insecticide", usages: "Pucerons, aleurodes", amm: "2150089" },
  { id: 6, nom: "Bacillus thuringiensis", substance: "B. thuringiensis", categorie: "Insecticide bio", usages: "Chenilles, larves", amm: "9600451" },
  { id: 7, nom: "Kaolin", substance: "Silicate d'aluminium", categorie: "Répulsif", usages: "Cicadelle, mouche olive", amm: "2110342" },
  { id: 8, nom: "Bicarbonate de potassium", substance: "K-HCO3", categorie: "Fongicide", usages: "Oïdium", amm: "2130198" },
];

const FERTILISANTS = [
  { id: 1, nom: "Fumier bovin composté", type: "Organique", statut: "autorise", azote: "3-5% N", restrictions: "Max 170 kg N/ha/an" },
  { id: 2, nom: "Compost végétal", type: "Organique", statut: "autorise", azote: "1-2% N", restrictions: "Aucune restriction spécifique" },
  { id: 3, nom: "Guano de chauve-souris", type: "Organique", statut: "autorise", azote: "5-10% N", restrictions: "Attestation fournisseur requise" },
  { id: 4, nom: "Farine de plumes", type: "Organique", statut: "conditionnel", azote: "12% N", restrictions: "Origine non industrielle requise" },
  { id: 5, nom: "Soufre (amendement)", type: "Minéral", statut: "autorise", azote: "-", restrictions: "Usage limité au pH" },
  { id: 6, nom: "Basalte broyé", type: "Minéral", statut: "autorise", azote: "-", restrictions: "Aucune" },
];

const INTERVENTIONS_INIT = [
  { id: 1, date: "2025-05-12", parcelle: "La Côte Sud", culture: "Maraîchage", produit: "Bouillie bordelaise", dose: "3 kg/ha", objectif: "Mildiou tomate", operateur: "Jean Martin" },
  { id: 2, date: "2025-04-28", parcelle: "Les Terrasses", culture: "Vigne", produit: "Soufre mouillable", dose: "5 kg/ha", objectif: "Oïdium vigne", operateur: "Jean Martin" },
];

const CERTIF_INIT = {
  organisme: "Ecocert",
  numero: "FR-BIO-01-2342",
  date_debut: "2021-01-15",
  date_prochain_audit: "2026-01-15",
  statut: "valide",
  productions: ["Grandes cultures", "Maraîchage"],
};

// ===================== COMPOSANTS COMMUNS =====================
function Modal({ title, onClose, children, footer }) {
  return (
    <div className="modal-overlay" onClick={e => e.target === e.currentTarget && onClose()}>
      <div className="modal">
        <div className="modal-header">
          <div className="modal-title">{title}</div>
          <button className="modal-close" onClick={onClose}>×</button>
        </div>
        <div className="modal-body">{children}</div>
        {footer && <div className="modal-footer">{footer}</div>}
      </div>
    </div>
  );
}

// ===================== DASHBOARD =====================
function Dashboard({ parcelles, interventions }) {
  const surfaceCertif = parcelles.filter(p => p.statut === "certifie").reduce((s, p) => s + p.surface, 0);
  const surfaceConv = parcelles.filter(p => p.statut === "conversion").reduce((s, p) => s + p.surface, 0);
  const today = new Date();
  const prochainAudit = new Date("2026-01-15");
  const joursAudit = Math.ceil((prochainAudit - today) / (1000*60*60*24));

  return (
    <div>
      <div className="stats-grid">
        <div className="stat-card">
          <div className="stat-emoji">🌿</div>
          <div className="stat-val">{surfaceCertif.toFixed(1)} ha</div>
          <div className="stat-label">Surfaces certifiées AB</div>
          <div className="stat-sub">✓ En production bio</div>
        </div>
        <div className="stat-card orange">
          <div className="stat-emoji">⏳</div>
          <div className="stat-val">{surfaceConv.toFixed(1)} ha</div>
          <div className="stat-label">En conversion</div>
          <div className="stat-sub">2 parcelles concernées</div>
        </div>
        <div className="stat-card terre">
          <div className="stat-emoji">🧪</div>
          <div className="stat-val">{interventions.length}</div>
          <div className="stat-label">Interventions 2025</div>
          <div className="stat-sub">Toutes produits AB</div>
        </div>
        <div className="stat-card alert">
          <div className="stat-emoji">📋</div>
          <div className="stat-val">{joursAudit}j</div>
          <div className="stat-label">Avant prochain audit</div>
          <div className="stat-sub">Ecocert – Jan. 2026</div>
        </div>
      </div>

      <div className="dash-grid">
        <div className="card">
          <div className="card-header">
            <div className="card-title">🌱 Dernières interventions</div>
          </div>
          <table>
            <thead>
              <tr>
                <th>Date</th>
                <th>Parcelle</th>
                <th>Produit</th>
                <th>Objectif</th>
              </tr>
            </thead>
            <tbody>
              {interventions.slice(-5).reverse().map(i => (
                <tr key={i.id}>
                  <td>{new Date(i.date).toLocaleDateString('fr-FR')}</td>
                  <td>{i.parcelle}</td>
                  <td><span className="badge badge-ab">🌿 {i.produit}</span></td>
                  <td style={{color:'#666', fontSize:'0.8rem'}}>{i.objectif}</td>
                </tr>
              ))}
              {interventions.length === 0 && (
                <tr><td colSpan="4"><div className="empty-state"><div className="empty-icon">📝</div><div className="empty-text">Aucune intervention enregistrée</div></div></td></tr>
              )}
            </tbody>
          </table>
        </div>

        <div style={{display:'flex', flexDirection:'column', gap:'16px'}}>
          <div className="card">
            <div className="card-header">
              <div className="card-title">⚠️ Alertes</div>
            </div>
            <div className="card-body">
              <div className="alert-item">
                <div className="alert-dot rouge"></div>
                <div>
                  <div className="alert-text">Audit Ecocert dans {joursAudit} jours — préparez vos documents</div>
                  <div className="alert-date">15 janvier 2026</div>
                </div>
              </div>
              <div className="alert-item">
                <div className="alert-dot orange"></div>
                <div>
                  <div className="alert-text">Champ du Moulin — fin de conversion dans 9 mois</div>
                  <div className="alert-date">Mars 2026</div>
                </div>
              </div>
              <div className="alert-item">
                <div className="alert-dot vert"></div>
                <div>
                  <div className="alert-text">Certiphyto à renouveler (optionnel en AB)</div>
                  <div className="alert-date">Juin 2026</div>
                </div>
              </div>
            </div>
          </div>

          <div className="card">
            <div className="card-header">
              <div className="card-title">📊 Surfaces</div>
            </div>
            <div className="card-body">
              <div style={{marginBottom:'12px'}}>
                <div style={{display:'flex',justifyContent:'space-between',fontSize:'0.82rem',marginBottom:'4px'}}>
                  <span>Certifié AB</span><strong style={{color:'var(--vert-moyen)'}}>{surfaceCertif.toFixed(1)} ha</strong>
                </div>
                <div className="conv-bar-wrap">
                  <div className="conv-bar" style={{width: `${surfaceCertif/(surfaceCertif+surfaceConv)*100}%`}}></div>
                </div>
              </div>
              <div>
                <div style={{display:'flex',justifyContent:'space-between',fontSize:'0.82rem',marginBottom:'4px'}}>
                  <span>En conversion</span><strong style={{color:'var(--or)'}}>{surfaceConv.toFixed(1)} ha</strong>
                </div>
                <div className="conv-bar-wrap">
                  <div className="conv-bar" style={{width:`${surfaceConv/(surfaceCertif+surfaceConv)*100}%`, background:'linear-gradient(90deg, var(--or), var(--terre-clair))'}}></div>
                </div>
              </div>
              <div style={{fontSize:'0.78rem',color:'#888',marginTop:'12px',textAlign:'center'}}>
                Total : {(surfaceCertif+surfaceConv).toFixed(1)} ha gérés
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

// ===================== PARCELLES =====================
function Parcelles({ parcelles, setParcelles }) {
  const [modal, setModal] = useState(false);
  const [form, setForm] = useState({ nom:'', surface:'', culture:'', statut:'certifie', debut_conversion:'', organisme:'Ecocert' });

  const getProgression = (debut) => {
    const d = new Date(debut);
    const now = new Date();
    const mois = Math.floor((now - d) / (1000*60*60*24*30));
    const duree = 24; // 2 ans grandes cultures
    return Math.min(100, Math.round(mois/duree*100));
  };

  const getFinConversion = (debut) => {
    const d = new Date(debut);
    d.setFullYear(d.getFullYear() + 2);
    return d.toLocaleDateString('fr-FR', {month:'long', year:'numeric'});
  };

  const ajouter = () => {
    if (!form.nom || !form.surface) return;
    setParcelles([...parcelles, { ...form, id: Date.now(), surface: parseFloat(form.surface) }]);
    setModal(false);
    setForm({ nom:'', surface:'', culture:'', statut:'certifie', debut_conversion:'', organisme:'Ecocert' });
  };

  return (
    <div>
      <div className="card">
        <div className="card-header">
          <div className="card-title">🗺️ Mes parcelles ({parcelles.length})</div>
          <button className="btn btn-primary" onClick={() => setModal(true)}>+ Ajouter parcelle</button>
        </div>
        <table>
          <thead>
            <tr>
              <th>Parcelle</th>
              <th>Culture</th>
              <th>Surface</th>
              <th>Statut</th>
              <th>Organisme</th>
              <th>Progression</th>
            </tr>
          </thead>
          <tbody>
            {parcelles.map(p => (
              <tr key={p.id}>
                <td><strong>{p.nom}</strong></td>
                <td>{p.culture}</td>
                <td>{p.surface} ha</td>
                <td>
                  {p.statut === 'certifie'
                    ? <span className="badge badge-ab">✅ Certifié AB</span>
                    : <span className="badge badge-conv">⏳ En conversion</span>}
                </td>
                <td style={{fontSize:'0.82rem',color:'#666'}}>{p.organisme}</td>
                <td style={{minWidth:'160px'}}>
                  {p.statut === 'conversion' ? (
                    <div>
                      <div className="conv-bar-wrap">
                        <div className="conv-bar" style={{width:`${getProgression(p.debut_conversion)}%`, background:'linear-gradient(90deg,var(--or),var(--terre-clair))'}}></div>
                      </div>
                      <div style={{fontSize:'0.72rem',color:'#888',marginTop:3}}>
                        {getProgression(p.debut_conversion)}% — certif. {getFinConversion(p.debut_conversion)}
                      </div>
                    </div>
                  ) : <span style={{fontSize:'0.82rem',color:'var(--vert-clair)'}}>✓ Certifié</span>}
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>

      {modal && (
        <Modal title="➕ Nouvelle parcelle" onClose={() => setModal(false)}
          footer={<><button className="btn btn-outline" onClick={() => setModal(false)}>Annuler</button><button className="btn btn-primary" onClick={ajouter}>Enregistrer</button></>}>
          <div className="form-grid">
            <div className="form-row">
              <div className="form-group">
                <label>Nom de la parcelle *</label>
                <input value={form.nom} onChange={e=>setForm({...form,nom:e.target.value})} placeholder="Ex: Le Grand Pré" />
              </div>
              <div className="form-group">
                <label>Surface (ha) *</label>
                <input type="number" step="0.1" value={form.surface} onChange={e=>setForm({...form,surface:e.target.value})} placeholder="Ex: 3.5" />
              </div>
            </div>
            <div className="form-row">
              <div className="form-group">
                <label>Culture principale</label>
                <input value={form.culture} onChange={e=>setForm({...form,culture:e.target.value})} placeholder="Ex: Blé tendre, Maraîchage…" />
              </div>
              <div className="form-group">
                <label>Statut AB</label>
                <select value={form.statut} onChange={e=>setForm({...form,statut:e.target.value})}>
                  <option value="certifie">Certifié AB</option>
                  <option value="conversion">En conversion</option>
                </select>
              </div>
            </div>
            <div className="form-row">
              <div className="form-group">
                <label>Date de début conversion</label>
                <input type="date" value={form.debut_conversion} onChange={e=>setForm({...form,debut_conversion:e.target.value})} />
              </div>
              <div className="form-group">
                <label>Organisme certificateur</label>
                <select value={form.organisme} onChange={e=>setForm({...form,organisme:e.target.value})}>
                  <option>Ecocert</option>
                  <option>Bureau Veritas</option>
                  <option>Certipaq</option>
                  <option>Afocert</option>
                  <option>Ocacia</option>
                  <option>Autre</option>
                </select>
              </div>
            </div>
          </div>
        </Modal>
      )}
    </div>
  );
}

// ===================== REGISTRE INTRANTS =====================
function RegistreIntrants({ interventions, setInterventions, parcelles }) {
  const [modal, setModal] = useState(false);
  const [tab, setTab] = useState('registre');
  const [recherche, setRecherche] = useState('');
  const [form, setForm] = useState({ date:'', parcelle:'', produit:'', dose:'', objectif:'', operateur:'' });

  const produitsFiltres = INTRANTS_AB.filter(p =>
    p.nom.toLowerCase().includes(recherche.toLowerCase()) ||
    p.substance.toLowerCase().includes(recherche.toLowerCase()) ||
    p.usages.toLowerCase().includes(recherche.toLowerCase())
  );

  const ajouter = () => {
    if (!form.date || !form.parcelle || !form.produit) return;
    const parc = parcelles.find(p => p.nom === form.parcelle);
    setInterventions([...interventions, {
      ...form, id: Date.now(), culture: parc?.culture || ''
    }]);
    setModal(false);
    setForm({ date:'', parcelle:'', produit:'', dose:'', objectif:'', operateur:'' });
  };

  return (
    <div>
      <div className="tabs">
        <button className={`tab ${tab==='registre'?'active':''}`} onClick={()=>setTab('registre')}>📋 Registre des interventions</button>
        <button className={`tab ${tab==='produits'?'active':''}`} onClick={()=>setTab('produits')}>🌿 Produits autorisés AB</button>
        <button className={`tab ${tab==='fertilisants'?'active':''}`} onClick={()=>setTab('fertilisants')}>🌱 Fertilisants & Amendements</button>
      </div>

      {tab === 'registre' && (
        <div className="card">
          <div className="card-header">
            <div className="card-title">📋 Interventions phytosanitaires AB</div>
            <button className="btn btn-primary" onClick={()=>setModal(true)}>+ Nouvelle intervention</button>
          </div>
          <div className="info-box" style={{margin:'0 20px 0', borderRadius:'8px 8px 0 0'}}>
            💡 <strong>Rappel :</strong> En agriculture biologique, seuls les produits listés dans l'Annexe I du règlement UE 2021/1165 et disposant d'une AMM française sont autorisés.
          </div>
          <table>
            <thead>
              <tr><th>Date</th><th>Parcelle</th><th>Culture</th><th>Produit AB utilisé</th><th>Dose</th><th>Objectif</th><th>Opérateur</th></tr>
            </thead>
            <tbody>
              {interventions.map(i => (
                <tr key={i.id}>
                  <td>{new Date(i.date).toLocaleDateString('fr-FR')}</td>
                  <td>{i.parcelle}</td>
                  <td style={{fontSize:'0.82rem',color:'#666'}}>{i.culture}</td>
                  <td><span className="badge badge-ab">🌿 {i.produit}</span></td>
                  <td style={{fontSize:'0.82rem'}}>{i.dose}</td>
                  <td style={{fontSize:'0.82rem',color:'#666'}}>{i.objectif}</td>
                  <td style={{fontSize:'0.82rem'}}>{i.operateur}</td>
                </tr>
              ))}
              {interventions.length === 0 && (
                <tr><td colSpan="7"><div className="empty-state"><div className="empty-icon">🌿</div><div className="empty-text">Aucune intervention enregistrée</div></div></td></tr>
              )}
            </tbody>
          </table>
        </div>
      )}

      {tab === 'produits' && (
        <div className="card">
          <div className="card-header">
            <div className="card-title">🌿 Produits autorisés en Agriculture Biologique</div>
            <span className="badge badge-ab">{INTRANTS_AB.length} produits</span>
          </div>
          <div className="card-body">
            <div className="info-box">
              ✅ Tous ces produits sont <strong>autorisés en AB</strong> conformément à l'Annexe I du règlement UE 2021/1165 et disposent d'une AMM pour la France. Vérifiez toujours la colonne "Production Biologique" sur e-phy.anses.fr avant utilisation.
            </div>
            <div className="search-box">
              <span className="search-icon">🔍</span>
              <input value={recherche} onChange={e=>setRecherche(e.target.value)} placeholder="Rechercher par nom, substance ou usage..." />
            </div>
            <div style={{display:'flex',flexDirection:'column',gap:'10px'}}>
              {produitsFiltres.map(p => (
                <div key={p.id} className="produit-item">
                  <div className="produit-ab">🌿</div>
                  <div className="produit-info">
                    <div className="produit-nom">{p.nom}</div>
                    <div className="produit-substance">Substance : {p.substance} · Catégorie : {p.categorie}</div>
                    <div style={{fontSize:'0.78rem',color:'var(--vert-clair)',marginTop:2}}>Usages : {p.usages}</div>
                  </div>
                  <div style={{textAlign:'right'}}>
                    <span className="badge badge-ab">AMM {p.amm}</span>
                    <div style={{fontSize:'0.7rem',color:'#aaa',marginTop:4}}>e-phy vérifié</div>
                  </div>
                </div>
              ))}
              {produitsFiltres.length === 0 && (
                <div className="empty-state"><div className="empty-icon">🔍</div><div className="empty-text">Aucun produit trouvé pour "{recherche}"</div></div>
              )}
            </div>
          </div>
        </div>
      )}

      {tab === 'fertilisants' && (
        <div className="card">
          <div className="card-header">
            <div className="card-title">🌱 Matières fertilisantes autorisées AB</div>
          </div>
          <div className="card-body">
            <div className="info-box">
              📋 Ces fertilisants sont conformes à l'<strong>Annexe II du règlement UE 2021/1165</strong>. La quantité d'azote épandu sous forme d'effluents d'élevage ne peut dépasser <strong>170 kg N/ha/an</strong>.
            </div>
          </div>
          <table>
            <thead>
              <tr><th>Intrant</th><th>Type</th><th>Statut AB</th><th>Teneur azote</th><th>Restrictions</th></tr>
            </thead>
            <tbody>
              {FERTILISANTS.map(f => (
                <tr key={f.id}>
                  <td><strong>{f.nom}</strong></td>
                  <td style={{fontSize:'0.82rem',color:'#666'}}>{f.type}</td>
                  <td>
                    <span className={`fertil-badge ${f.statut === 'autorise' ? 'fertil-autorise' : 'fertil-conditionnel'}`}>
                      {f.statut === 'autorise' ? '✅ Autorisé' : '⚠️ Conditionnel'}
                    </span>
                  </td>
                  <td style={{fontSize:'0.82rem'}}>{f.azote}</td>
                  <td style={{fontSize:'0.78rem',color:'#777'}}>{f.restrictions}</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      )}

      {modal && (
        <Modal title="🌿 Nouvelle intervention AB" onClose={()=>setModal(false)}
          footer={<><button className="btn btn-outline" onClick={()=>setModal(false)}>Annuler</button><button className="btn btn-primary" onClick={ajouter}>Enregistrer</button></>}>
          <div className="form-grid">
            <div className="form-row">
              <div className="form-group">
                <label>Date *</label>
                <input type="date" value={form.date} onChange={e=>setForm({...form,date:e.target.value})} />
              </div>
              <div className="form-group">
                <label>Parcelle *</label>
                <select value={form.parcelle} onChange={e=>setForm({...form,parcelle:e.target.value})}>
                  <option value="">-- Choisir --</option>
                  {parcelles.map(p => <option key={p.id} value={p.nom}>{p.nom}</option>)}
                </select>
              </div>
            </div>
            <div className="form-group">
              <label>Produit AB utilisé *</label>
              <select value={form.produit} onChange={e=>setForm({...form,produit:e.target.value})}>
                <option value="">-- Choisir un produit autorisé AB --</option>
                {INTRANTS_AB.map(p => <option key={p.id} value={p.nom}>{p.nom} ({p.categorie})</option>)}
              </select>
            </div>
            <div className="form-row">
              <div className="form-group">
                <label>Dose appliquée</label>
                <input value={form.dose} onChange={e=>setForm({...form,dose:e.target.value})} placeholder="Ex: 3 kg/ha" />
              </div>
              <div className="form-group">
                <label>Opérateur</label>
                <input value={form.operateur} onChange={e=>setForm({...form,operateur:e.target.value})} placeholder="Nom de l'applicateur" />
              </div>
            </div>
            <div className="form-group">
              <label>Objectif / Cible visée</label>
              <input value={form.objectif} onChange={e=>setForm({...form,objectif:e.target.value})} placeholder="Ex: Mildiou tomate, pucerons…" />
            </div>
          </div>
        </Modal>
      )}
    </div>
  );
}

// ===================== CERTIFICATION =====================
function Certification() {
  const certif = CERTIF_INIT;
  const today = new Date();
  const audit = new Date(certif.date_prochain_audit);
  const jours = Math.ceil((audit - today) / (1000*60*60*24));

  const DOCS_AUDIT = [
    { nom: "Registre des interventions phytosanitaires", fait: true },
    { nom: "Registre des fertilisants utilisés", fait: true },
    { nom: "Cahier de récolte et de stockage", fait: false },
    { nom: "Factures/BL des intrants de l'année", fait: false },
    { nom: "Contrats de vente (traçabilité aval)", fait: true },
    { nom: "Carte des parcelles (TéléPAC / CartoBio)", fait: true },
    { nom: "Registre de nettoyage des équipements", fait: false },
  ];

  const faitCount = DOCS_AUDIT.filter(d => d.fait).length;

  return (
    <div>
      <div className="grid-2" style={{marginBottom:'20px'}}>
        <div className="card">
          <div className="card-header">
            <div className="card-title">🏆 Ma certification AB</div>
            <span className="badge badge-ab">✅ Valide</span>
          </div>
          <div className="card-body">
            <div className="certif-card">
              <div className="certif-org">{certif.organisme}</div>
              <div className="certif-num">{certif.numero}</div>
              <div className="certif-info" style={{marginTop:8}}>
                <div>📅 Début : {new Date(certif.date_debut).toLocaleDateString('fr-FR')}</div>
                <div style={{marginTop:4}}>🔄 Prochain audit : <strong style={{color: jours < 90 ? 'var(--rouge-bio)' : 'var(--vert-moyen)'}}>
                  {new Date(certif.date_prochain_audit).toLocaleDateString('fr-FR')} ({jours} jours)
                </strong></div>
              </div>
              <div style={{marginTop:12, display:'flex', gap:8, flexWrap:'wrap'}}>
                {certif.productions.map(p => <span key={p} className="badge badge-neutre">{p}</span>)}
              </div>
            </div>
          </div>
        </div>

        <div className="card">
          <div className="card-header">
            <div className="card-title">📋 Préparation audit</div>
            <span className="badge badge-conv">{faitCount}/{DOCS_AUDIT.length} docs</span>
          </div>
          <div className="card-body">
            <div className="conv-bar-wrap" style={{marginBottom:12}}>
              <div className="conv-bar" style={{width:`${faitCount/DOCS_AUDIT.length*100}%`}}></div>
            </div>
            <div style={{display:'flex',flexDirection:'column',gap:8}}>
              {DOCS_AUDIT.map((d,i) => (
                <div key={i} style={{display:'flex',alignItems:'center',gap:10,fontSize:'0.85rem'}}>
                  <span style={{fontSize:'1rem'}}>{d.fait ? '✅' : '⬜'}</span>
                  <span style={{color: d.fait ? 'var(--gris-texte)' : '#999', textDecoration: d.fait ? 'none' : 'none'}}>{d.nom}</span>
                </div>
              ))}
            </div>
          </div>
        </div>
      </div>

      <div className="card">
        <div className="card-header">
          <div className="card-title">📅 Organismes certificateurs AB en France</div>
        </div>
        <table>
          <thead>
            <tr><th>Organisme</th><th>Code</th><th>Site</th><th>Spécialité</th></tr>
          </thead>
          <tbody>
            {[
              { nom: "Ecocert", code: "FR-BIO-01", site: "ecocert.com", spec: "Généraliste" },
              { nom: "Bureau Veritas", code: "FR-BIO-04", site: "bureauveritas.fr", spec: "Généraliste" },
              { nom: "Certipaq", code: "FR-BIO-09", site: "certipaq.com", spec: "Élevage, Grandes cultures" },
              { nom: "Afocert", code: "FR-BIO-14", site: "afocert.fr", spec: "Généraliste" },
              { nom: "Ocacia", code: "FR-BIO-17", site: "ocacia.fr", spec: "Généraliste" },
            ].map(o => (
              <tr key={o.code}>
                <td><strong>{o.nom}</strong></td>
                <td><span className="badge badge-neutre">{o.code}</span></td>
                <td style={{fontSize:'0.82rem',color:'var(--vert-clair)'}}>{o.site}</td>
                <td style={{fontSize:'0.82rem',color:'#666'}}>{o.spec}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
}

// ===================== AIDES PAC BIO =====================
function AidesPAC() {
  const AIDES = [
    { nom: "Aide au maintien AB", code: "MAB", montant: "110 €/ha", duree: "5 ans (2023-2027)", statut: "engage", surface: 7.0, desc: "Prairies, grandes cultures" },
    { nom: "Aide à la conversion AB", code: "CAB", montant: "180 €/ha (1ères années)", duree: "2 ans conversion", statut: "en_cours", surface: 8.4, desc: "Parcelles en conversion" },
    { nom: "MAEC systèmes polyculture-élevage bio", code: "MAEC-SYS", montant: "Variable", duree: "5 ans", statut: "non_engage", surface: 0, desc: "Selon territoire" },
    { nom: "Écorégime voie bio (PAC)", code: "ECO-BIO", montant: "145 €/ha", duree: "Annuelle", statut: "engage", surface: 15.4, desc: "100% exploitation en AB" },
  ];

  const getBadge = (s) => {
    if (s === 'engage') return <span className="badge badge-ab">✅ Engagé</span>;
    if (s === 'en_cours') return <span className="badge badge-conv">⏳ En cours</span>;
    return <span className="badge badge-neutre">— Non engagé</span>;
  };

  const totalAnnuel = 110*7 + 180*8.4 + 145*15.4;

  return (
    <div>
      <div className="grid-3" style={{marginBottom:'20px'}}>
        <div className="stat-card">
          <div className="stat-emoji">💶</div>
          <div className="stat-val">~{Math.round(totalAnnuel).toLocaleString('fr-FR')} €</div>
          <div className="stat-label">Aides AB estimées / an</div>
          <div className="stat-sub">Hors variations PAC</div>
        </div>
        <div className="stat-card orange">
          <div className="stat-emoji">📄</div>
          <div className="stat-val">2027</div>
          <div className="stat-label">Fin du PSN en cours</div>
          <div className="stat-sub">Renouvellement à anticiper</div>
        </div>
        <div className="stat-card terre">
          <div className="stat-emoji">🗓️</div>
          <div className="stat-val">15 mai</div>
          <div className="stat-label">Date limite déclaration PAC</div>
          <div className="stat-sub">Via TéléPAC chaque année</div>
        </div>
      </div>

      <div className="card">
        <div className="card-header">
          <div className="card-title">💶 Aides PAC liées à l'agriculture biologique</div>
        </div>
        <div className="card-body">
          <div className="info-box">
            📋 Ces aides font partie du <strong>Plan Stratégique National (PSN) 2023-2027</strong>. Les engagements sont sur 5 ans. La demande se fait annuellement via <strong>TéléPAC</strong> avant le 15 mai. Pensez à cocher la case <strong>CartoBio</strong> pour simplifier vos démarches auprès de votre organisme certificateur.
          </div>
        </div>
        <table>
          <thead>
            <tr><th>Aide</th><th>Code</th><th>Montant unitaire</th><th>Durée</th><th>Surface</th><th>Statut</th></tr>
          </thead>
          <tbody>
            {AIDES.map((a,i) => (
              <tr key={i}>
                <td>
                  <strong>{a.nom}</strong>
                  <div style={{fontSize:'0.75rem',color:'#888',marginTop:2}}>{a.desc}</div>
                </td>
                <td><span className="badge badge-neutre">{a.code}</span></td>
                <td style={{fontWeight:600,color:'var(--vert-moyen)'}}>{a.montant}</td>
                <td style={{fontSize:'0.82rem',color:'#666'}}>{a.duree}</td>
                <td>{a.surface > 0 ? `${a.surface} ha` : '—'}</td>
                <td>{getBadge(a.statut)}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
}

// ===================== CONSEILLER IA =====================
function ConseillerIA() {
  const [messages, setMessages] = useState([
    { role: 'assistant', text: "Bonjour ! Je suis votre conseiller spécialisé en agriculture biologique. Posez-moi vos questions sur la réglementation AB, les intrants autorisés, les périodes de conversion, ou les aides PAC. ⚠️ Mes réponses sont indicatives et ne remplacent pas l'avis de votre organisme certificateur." }
  ]);
  const [input, setInput] = useState('');
  const [loading, setLoading] = useState(false);

  const envoyer = async () => {
    if (!input.trim() || loading) return;
    const question = input.trim();
    setInput('');
    setMessages(prev => [...prev, { role: 'user', text: question }]);
    setLoading(true);

    try {
      const response = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 1000,
          system: "Tu es un conseiller expert en agriculture biologique française. Tu réponds en français de façon claire, pratique et bienveillante. Tu connais parfaitement le règlement UE 2021/1165, le règlement UE 2018/848, les aides PAC-AB, les organismes certificateurs français (Ecocert, Bureau Veritas, Certipaq, Afocert, Ocacia), et les pratiques agronomiques biologiques. Termine toujours tes réponses par un rappel que tes informations sont indicatives et que l'agriculteur doit consulter son organisme certificateur pour toute décision réglementaire.",
          messages: [{ role: "user", content: question }]
        })
      });
      const data = await response.json();
      const rep = data.content?.[0]?.text || "Je n'ai pas pu obtenir de réponse.";
      setMessages(prev => [...prev, { role: 'assistant', text: rep }]);
    } catch(e) {
      setMessages(prev => [...prev, { role: 'assistant', text: "Erreur de connexion. Vérifiez votre accès internet." }]);
    }
    setLoading(false);
  };

  return (
    <div className="card" style={{display:'flex',flexDirection:'column',height:'calc(100vh - 180px)'}}>
      <div className="card-header">
        <div className="card-title">🤖 Conseiller IA – Agriculture Biologique</div>
        <span className="badge badge-neutre">Bêta</span>
      </div>
      <div style={{flex:1,overflow:'auto',padding:'20px 24px',display:'flex',flexDirection:'column',gap:12}}>
        {messages.map((m,i) => (
          <div key={i} style={{
            display:'flex', justifyContent: m.role === 'user' ? 'flex-end' : 'flex-start'
          }}>
            <div style={{
              maxWidth:'75%',
              padding:'12px 16px',
              borderRadius: m.role === 'user' ? '16px 16px 4px 16px' : '16px 16px 16px 4px',
              background: m.role === 'user' ? 'var(--vert-moyen)' : 'var(--creme)',
              color: m.role === 'user' ? 'white' : 'var(--gris-texte)',
              fontSize:'0.875rem',
              lineHeight:1.6,
              border: m.role !== 'user' ? '1px solid var(--gris-clair)' : 'none'
            }}>
              {m.text}
            </div>
          </div>
        ))}
        {loading && (
          <div style={{display:'flex',gap:12,alignItems:'center'}}>
            <div style={{background:'var(--creme)',border:'1px solid var(--gris-clair)',borderRadius:'16px 16px 16px 4px',padding:'12px 16px',color:'#888',fontSize:'0.85rem'}}>
              🌿 Réflexion en cours…
            </div>
          </div>
        )}
      </div>
      <div style={{padding:'16px 24px',borderTop:'1px solid var(--gris-clair)',display:'flex',gap:10}}>
        <input
          style={{flex:1}}
          value={input}
          onChange={e=>setInput(e.target.value)}
          onKeyDown={e=>e.key==='Enter' && envoyer()}
          placeholder="Ex: Le cuivre est-il autorisé en AB sur vigne ? Quelle est la dose max ?"
          disabled={loading}
        />
        <button className="btn btn-primary" onClick={envoyer} disabled={loading || !input.trim()}>
          Envoyer
        </button>
      </div>
    </div>
  );
}

// ===================== APP PRINCIPALE =====================
const MODULES = [
  { id: 'dashboard', label: 'Tableau de bord', icon: '🏠' },
  { id: 'parcelles', label: 'Mes parcelles', icon: '🗺️' },
  { id: 'intrants', label: 'Registre intrants', icon: '🌿' },
  { id: 'certification', label: 'Certification AB', icon: '🏆' },
  { id: 'aides', label: 'Aides PAC Bio', icon: '💶' },
  { id: 'conseiller', label: 'Conseiller IA', icon: '🤖' },
];

function App() {
  const [module, setModule] = useState('dashboard');
  const [parcelles, setParcelles] = useState(PARCELLES_INIT);
  const [interventions, setInterventions] = useState(INTERVENTIONS_INIT);

  const titres = {
    dashboard: 'Tableau de bord',
    parcelles: 'Mes parcelles',
    intrants: 'Registre des intrants',
    certification: 'Certification AB',
    aides: 'Aides PAC Biologique',
    conseiller: 'Conseiller IA',
  };

  return (
    <div>
      <aside className="sidebar">
        <div className="logo-zone">
          <div className="logo-title">Facil<span>Bio</span></div>
          <div className="logo-sub">Gestion Agriculture Bio</div>
          <div className="label-ab">🌿 Agriculture Biologique</div>
        </div>
        <nav className="nav-section">
          <div className="nav-label">Navigation</div>
          {MODULES.map(m => (
            <div key={m.id} className={`nav-item ${module===m.id?'active':''}`} onClick={()=>setModule(m.id)}>
              <span className="nav-icon">{m.icon}</span>
              {m.label}
            </div>
          ))}
        </nav>
        <div className="sidebar-bottom">
          FacilBio v0.1 · Facil'Gestion31<br/>
          Régl. UE 2021/1165 · 2018/848
        </div>
      </aside>

      <main className="main">
        <div className="topbar">
          <div className="page-title">{titres[module]}</div>
          <div className="topbar-right">
            <span className="badge badge-ab">🌿 Mode Agriculture Biologique</span>
          </div>
        </div>
        <div className="content">
          {module === 'dashboard' && <Dashboard parcelles={parcelles} interventions={interventions} />}
          {module === 'parcelles' && <Parcelles parcelles={parcelles} setParcelles={setParcelles} />}
          {module === 'intrants' && <RegistreIntrants interventions={interventions} setInterventions={setInterventions} parcelles={parcelles} />}
          {module === 'certification' && <Certification />}
          {module === 'aides' && <AidesPAC />}
          {module === 'conseiller' && <ConseillerIA />}
        </div>
      </main>
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
</script>
</body>
</html>
# FacilBio

<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
 
</head>
<body>

  <h1>📦 WordPress + MySQL sur Kubernetes</h1>

  <p>Ce projet déploie une stack WordPress complète avec une base de données MySQL dans un cluster Kubernetes. Il inclut la configuration des services, déploiements, et secrets nécessaires.</p>

  <h2>📁 Fichiers inclus</h2>
  <table>
    <tr>
      <th>Fichier</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>mysql-secret.yml</code></td>
      <td>Secret Kubernetes contenant le mot de passe MySQL</td>
    </tr>
    <tr>
      <td><code>mysql-deployment.yml</code></td>
      <td>Déploiement du pod MySQL</td>
    </tr>
    <tr>
      <td><code>mysql-service.yml</code></td>
      <td>Service interne pour exposer MySQL à WordPress</td>
    </tr>
    <tr>
      <td><code>wordpress-deployment.yml</code></td>
      <td>Déploiement du pod WordPress</td>
    </tr>
    <tr>
      <td><code>wordpress-service.yml</code></td>
      <td>Service NodePort pour exposer WordPress</td>
    </tr>
  </table>

  <h2>🚀 Déploiement</h2>
  <p><strong>Prérequis :</strong> un cluster Kubernetes fonctionnel (<code>minikube</code>, <code>kind</code>, ou cloud)</p>

  <ol>
    <li><strong>Créer le secret MySQL</strong> :
      <pre><code>kubectl apply -f mysql-secret.yml</code></pre>
    </li>
    <li><strong>Déployer MySQL</strong> :
      <pre><code>kubectl apply -f mysql-deployment.yml
kubectl apply -f mysql-service.yml</code></pre>
    </li>
    <li><strong>Déployer WordPress</strong> :
      <pre><code>kubectl apply -f wordpress-deployment.yml
kubectl apply -f wordpress-service.yml</code></pre>
    </li>
    <li><strong>Accéder à WordPress</strong> :
      <p>Si tu es en local (ex: <code>minikube</code>), récupère le port exposé :</p>
      <pre><code>kubectl get svc wordpress</code></pre>
      <p>Puis ouvre dans ton navigateur :</p>
      <pre><code>http://localhost:&lt;nodePort&gt;</code></pre>
    </li>
  </ol>

  <h2>⚙️ Paramètres personnalisables</h2>
  <ul>
    <li><code>mysql-secret.yml</code> → mot de passe MySQL (<code>password</code>)</li>
    <li><code>wordpress-deployment.yml</code> → image WordPress, variables d’environnement</li>
    <li><code>mysql-deployment.yml</code> → image MySQL, base de données, utilisateur</li>
  </ul>

  <h2>📌 Notes</h2>
  <ul>
    <li>Ce projet utilise <code>hostPath</code> pour persister les données WordPress. En production, utilise des <strong>PersistentVolumeClaims</strong>.</li>
    <li>Le mot de passe est encodé en base64, mais non chiffré. Pour plus de sécurité, utilise un gestionnaire de secrets (Vault, AWS Secrets Manager, etc.).</li>
  </ul>

  <h2>🧼 Nettoyage</h2>
  <pre><code>kubectl delete -f .</code></pre>

</body>
</html>

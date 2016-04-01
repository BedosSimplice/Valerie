# Valerie
MZ
-- phpMyAdmin SQL Dump
-- version 4.5.1
-- http://www.phpmyadmin.net
--
-- Client :  127.0.0.1
-- Généré le :  Jeu 31 Mars 2016 à 15:21
-- Version du serveur :  10.1.10-MariaDB
-- Version de PHP :  7.0.2

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Base de données :  `chapitre`
--

-- --------------------------------------------------------

--
-- Structure de la table `auteurs`
--

CREATE TABLE `auteurs` (
  `id` int(10) UNSIGNED NOT NULL,
  `nom` varchar(50) DEFAULT NULL,
  `prenom` varchar(50) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


-- --------------------------------------------------------

--
-- Structure de la table `clients`
--

CREATE TABLE `clients` (
  `id` int(10) UNSIGNED NOT NULL,
  `email` varchar(80) NOT NULL,
  `password` varchar(45) NOT NULL
  `TélPortable` varchar(45) NOT NULL
  `adresse` varchar(45) NOT NULL
  `ville` varchar(45) NOT NULL
  `cp` varchar(45) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Contenu de la table `clients`
--

INSERT INTO `clients` (`id`, `email`, `password`) VALUES
(1, 'client@client.com', '40bd001563085fc35165329ea1ff5c5ecbdbbeef'),
(2, 'moi@moi.com', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(21, 'moi@moi.com2', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(24, 'moi@moi.com256fbaa814bc49', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(25, 'moi@moi.com256fbabaff31c2', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(26, 'moi@moi.com256fbac23e6451', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(27, 'moi@moi.com256fbb119602ce', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(28, 'moi@moi.com256fbb172c471a', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(29, 'moi@moi.com256fbddc643ba3', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(30, 'moi@moi.com256fbddd349864', '51eac6b471a284d3341d8c0c63d0f1a286262a18'),
(31, 'moi@moi.com256fbdddc6116c', '51eac6b471a284d3341d8c0c63d0f1a286262a18');

-- --------------------------------------------------------

--
-- Structure de la table `editeurs`
--

CREATE TABLE `produit` (
  `id` int(10) UNSIGNED NOT NULL,
  `produit` varchar(50) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Contenu de la table `produit`
--

INSERT INTO `produit` (`id`, `produit`) VALUES
(1, 'CARTON CUISSES POULET'),
(2, 'CARTON POISSON TILAPIA'),
(3, 'CARTON AILES POULET'),
(4, 'CARTON POISSON DORADES'),
(5, 'SAC DE RIZ'),
(6, 'PACT DE  JUS'),
(7, 'CARTON DE PLANTAIN'),
(8, 'SAC DE SEMOULE'),
(9, 'CARTON DE GOMBO'),
(10, 'CARTON AILES DINDE');

-- --------------------------------------------------------


INSERT INTO `produits` (`id`, `nom`, `prix`) VALUES
(1, 'CARTON CUISSES POULET', 20.00, 1, 1, 1),
(2, 'CARTON POISSON TILAPIA', 12.90, 2, 2, 1),
(3, 'CARTON AILES POULET', 22.00, 3, 3, 2),
(4, 'CARTON POISSON DORADES', 67.90, 3, 4, 2),
(5, 'SAC DE RIZ', 11.90, 1, 5, 1),
(6, 'PACT DE  JUS', 12.00, 3, 6, 3),
(7, 'CARTON DE PLANTAIN', 35.90, 3, 7, 3),
(8, 'SAC DE SEMOULE', 5.90, 4, 8, 1),
(9, 'CARTON DE GOMBO', 38.50, 4, 9, 1),
(10, 'CARTON AILES DINDE', 42.00, 3, 10, 3),


-- --------------------------------------------------------

--
-- Structure de la table `panier`
--

CREATE TABLE `panier` (
  `produit_id` int(10) UNSIGNED NOT NULL,
  `client_id` int(10) UNSIGNED NOT NULL,
  `qt` tinyint(3) UNSIGNED NOT NULL DEFAULT '1'
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Contenu de la table `panier`
--

INSERT INTO `panier` (`produit_id`, `client_id`, `qt`) VALUES
(1, 1, 4),
(2, 1, 1),
(3, 1, 1),
(4, 1, 1),
(5, 1, 1),
(8, 1, 1),
(9, 1, 1),
(15, 1, 1);

-- --------------------------------------------------------

--
-- Doublure de structure pour la vue `vue_catalogue`

CREATE TABLE `vue_catalogue` (
`id` int(10) unsigned
,`produit` varchar(100)
,`prix` float(5,2)
);


-- --------------------------------------------------------

--
-- Structure de la vue `vue_catalogue`
--
DROP TABLE IF EXISTS `vue_catalogue`;

CREATE ALGORITHM=UNDEFINED DEFINER=`root`@`localhost` SQL SECURITY DEFINER VIEW `vue_catalogue`  AS  select `produit`.`id` AS `id`,`produit`.`prix` AS `prix`,concat_ws(' ',`client`.`prenom`,`client`.`nom`) AS `nom_client`,`client`.`nom` AS `client` from (((`produit` join `panier` on((`client`.`id` = `produit`.`panier_id`))) join `client` on((`client`.`id` = `produit`.`client_id`)));

--
-- Index pour les tables exportées
--

--
-- Index pour la table `clients`
--
ALTER TABLE `clients`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `email_UNIQUE` (`email`);


--
-- Index pour la table `produit`
--
ALTER TABLE `produit`
  ADD PRIMARY KEY (`id`),
  ADD KEY `produit_to_panier` (`produit_id`);
  

--
-- Index pour la table `panier`
--
ALTER TABLE `panier`
  ADD PRIMARY KEY (`produit_id`,`client_id`),
  ADD KEY `panier_to_client_idx` (`client_id`);

--
-- AUTO_INCREMENT pour les tables exportées
--

--
-- AUTO_INCREMENT pour la table `panier`
--
ALTER TABLE `panier`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=18;
--
-- AUTO_INCREMENT pour la table `clients`
--
ALTER TABLE `clients`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=32;

--
-- AUTO_INCREMENT pour la table `produit`
--
ALTER TABLE `produit`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=35;
--
-- Contraintes pour les tables exportées
--

--
-- Contraintes pour la table `produit`
--
ALTER TABLE `produit`

  ADD CONSTRAINT `produit_to_panier` FOREIGN KEY (`produit_id`) REFERENCES `produit` (`id`);
  
--
-- Contraintes pour la table `panier`
--
ALTER TABLE `panier`
  ADD CONSTRAINT `panier_to_client` FOREIGN KEY (`client_id`) REFERENCES `clients` (`id`) ON DELETE NO ACTION ON UPDATE NO ACTION,
  ADD CONSTRAINT `panier_to_produit` FOREIGN KEY (`produit_id`) REFERENCES `produit` (`id`) ON DELETE NO ACTION ON UPDATE NO ACTION;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

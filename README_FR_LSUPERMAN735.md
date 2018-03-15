<h1 align="center">Roact</h1>
<div align="center">
	<a href="https://travis-ci.org/Roblox/roact">
		<img src="https://api.travis-ci.org/Roblox/roact.svg?branch=master" alt="Travis-CI Build Status" />
	</a>
	<a href="https://coveralls.io/github/Roblox/roact?branch=master">
		<img src="https://coveralls.io/repos/github/Roblox/roact/badge.svg?branch=master" alt="Coveralls Coverage" />
	</a>
	<a href="https://roblox.github.io/roact">
		<img src="https://img.shields.io/badge/docs-website-green.svg" alt="Documentation" />
	</a>
</div>

<div align="center">
	Une bibliothèque de vues déclarative pour Roblox Lua inspirée par <a href="https://reactjs.org">React</a>.
</div>

<div>&nbsp;</div>

## Installation

### Méthode 1 : Script d'Installation  (Roblox Studio)
* Télécharger la dernière version depuis la [GitHub releases page](https://github.com/Roblox/Roact/releases).
* Utilisez le menu 'Exécuter le script' (situé dans l'onglet Test) pour localiser et exécuter ce script.
* Suivez les instructions dans le programme d'installation

Ce script d'installation est généré par un outil appelé [rbxpacker](https://github.com/LPGhatguy/rbxpacker).

### Méthode 2 : Système de fichiers
* Copiez le répertoire `lib` dans votre base de code
* Renommez le dossier à `Roact`
* Utilisez un plugin comme [Rojo] (https://github.com/LPGhatguy/rojo) pour synchroniser les fichiers dans un endroit

## Usage
Cet exemple crée un `TextLabel` en plein écran avec un message d'accueil.

Pour des exemples plus détaillés, consultez [la documentation] (#).

```lua
local LocalPlayer = game:GetService("Players").LocalPlayer

local Roact = require(Roact)

-- Définir un composant fonctionnel
local function HelloComponent()
	-- createElement prend trois arguments :
	-- * Le type d'élément à faire
        -- * Éventuellement, une liste de propriétés à fournir
        -- * Facultativement, un dictionnaire d'enfants. La clé est le nom de cet enfant

	return Roact.createElement("ScreenGui", {
	}, {
		MainLabel = Roact.createElement("TextLabel", {
			Text = "Hello, world!",
			Size = UDim2.new(1, 0, 1, 0),
		}),
	})
end

-- Créez notre arbre virtuel
local root = Roact.createElement(HelloComponent)

-- Transformez notre arbre virtuel en instances réelles et placez-les PlayerGui
Roact.reify(root, LocalPlayer.PlayerGui, "HelloWorld")
```

Nous pouvons aussi écrire cet exemple en utilisant un *stateful* composant:

```lua
local LocalPlayer = game:GetService("Players").LocalPlayer

local Roact = require(Roact)

-- Créez notre type de composant
local HelloComponent = Roact.Component:extend("HelloComponent")

-- 'render' DOIT être substitué.
function HelloComponent:render()
	-- createElement prend trois arguments :
	-- * Le type d'élément à faire
        -- * Éventuellement, une liste de propriétés à fournir
        -- * Facultativement, un dictionnaire d'enfants. La clé est le nom de cet enfant

	return Roact.createElement("ScreenGui", {
	}, {
		MainLabel = Roact.createElement("TextLabel", {
			Text = "Hello, world!",
			Size = UDim2.new(1, 0, 1, 0),
		}),
	})
end

-- Créez notre arbre virtuel
local root = Roact.createElement(HelloComponent)

-- Transformez notre arbre virtuel en instances réelles et placez-les PlayerGui
Roact.reify(root, LocalPlayer.PlayerGui, "HelloWorld")
```

## Licence
Roact est disponible sous la licence Apache 2.0. Voir [LICENCE] (LICENCE) pour plus de détails.

node("master") {
	stage 'Pull changes'
	checkout scm

	stage 'Build GDD'
	dir('gdd') {
		sh 'pdflatex index.tex'
		sh 'cp index.pdf Colobot_Gold_Edition-Game_Design_Document.pdf'
		archive 'Colobot_Gold_Edition-Game_Design_Document.pdf'
	}
}

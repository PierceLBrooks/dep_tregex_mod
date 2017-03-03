all:
	sphinx-build . html
	rm -Rf ../docs/*
	mv -f html/* ../docs
	rm -Rf html
	touch ../docs/.nojekyll

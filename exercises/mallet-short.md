
1. Install Java: https://www.oracle.com/java/technologies/downloads Choose your OS and the right installer.
2. Go to the terminal, check it is installed: `javac`
3. Download Mallet: https://mallet.cs.umass.edu/download.php
4. Unzip the folder in your user folder. In my case it was: /Users/susannalles/mallet-2.0.8
5. Go to your terminal, and place yourself in the folder mallet-2.0.8
6. Check Mallet is working: `bin/mallet import-dir --help`


To work with sample data, run in the command line (we need to be in the mallet-2.0.8 folder):

`bin/mallet import-dir --input sample-data/web/en --output tutorial.mallet --keep-sequence --remove-stopwords`

`bin/mallet train-topics --input tutorial.mallet` 

To work with Lindsay's folder, run in the command line (we need to be in the mallet-2.0.8 folder):

`bin/mallet import-dir --input we1s-data --output we1s.mallet --keep-sequence --remove-stopwords`

`bin/mallet train-topics --input we1s.mallet` 

These are more advanced commands that will generete some files: 

`bin/mallet train-topics --input we1s.mallet --num-topics 25 --optimize-interval 10 --output-state we1s-topic-state.gz --output-topic-keys we1s-keys.txt --output-doc-topics we1s-composition.txt --word-topic-counts-file we1s-topic-counts.txt --diagnostics-file we1s-diagnostics.xml`

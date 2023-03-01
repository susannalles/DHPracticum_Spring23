---
layout: page
title: Topic Modeling Tutorial
---
By Lindsay Thomas
# Topic Modeling with MALLET
## 1. Install MALLET: Please complete before class on Thursday, March 9
The good news about using MALLET is that installing it on your computer is the hardest part. Here are some links to tutorials that include good installation instructions for both Windows and Mac machines:

- ["Getting Started with Topic Modeling and MALLET," by Shawn Graham, Scott Weingart, and Ian Milligan, *Programming Historian*](http://programminghistorian.org/en/lessons/topic-modeling-and-mallet){:target="_blank"}: The OG DH MALLET tutorial. Follow the instructions under "Installing MALLET." Includes detailed installation instructions for both Windows and Mac, including screenshots, but was posted over 10 years now, so some things are likely out of date.
- ["Topic Modeling -- Set Up," by Melanie Walsh, *Introduction to Cultural Analytics & Python*](https://melaniewalsh.github.io/Intro-Cultural-Analytics/05-Text-Analysis/07-Topic-Modeling-Set-Up.html){:target="_blank"}: Published in 2021, the best more recent MALLET installation instructions for Windows and Mac that I've found. Follow the instructions for your type of machine until the "Install Little MALLET Wrapper" instructions (we aren't doing that, so you don't need to worry about installing the wrapper).

If you're using a Mac computer, make sure to unzip the `mallet-2.0.8` file in  your home (i.e., user) folder. If you're using a Windows machine, move it into your `C:\` drive. For Windows machines, MALLET will not work if it is not located directly in your `C:\` drive (i.e., do not put it in another folder inside your `C:\` drive).

To check if you've installed MALLET correctly:
1. Navigate in the command prompt/terminal to your `mallet-2.0.8` folder.
2. From within that folder, in the command prompt/terminal, type `bin\mallet` (Windows) or `bin/mallet` (Mac). If MALLET is installed correctly on your computer, you will now see a list of MALLET commands. If it isn't installed correctly, you'll see an error message. Check to make sure that you've typed the command correctly, that you're actually located within the MALLET folder, and that you set up your environment variable correctly.
3. Finally, read the part of the [*Programming Historian* MALLET tutorial](http://programminghistorian.org/en/lessons/topic-modeling-and-mallet){:target="_blank"} titled "Typing in MALLET Commands."

## 2. Download our Data
I've provided you with a zip file of 1000 text files drawn from the [WhatEvery1Says project data](https://we1s.ucsb.edu/research/we1s-materials/datasets/){:target="_blank"}. This folder includes 500 newspaper articles classified as being about the humanities and 500 newspaper articles as being classified about science (if you took my class last spring you worked with this data in our Voyant lab). **Unzip this file in the `mallet-2.0.8` folder you just downloaded and installed.** This means that your MALLET folder should now also include an unzipped folder titled `we1s-data` that includes the text files we will use in this tutorial.

## 3. Import the Data
To work with text data in MALLET, we first have to transform our corpus of text files into a MALLET format file. We do this using the `import` command. We will discuss the components of this command during class on March 9.

Making sure you are in the `mallet-2.0.8` folder, type the below command:

Windows:
`bin\mallet import-dir --input we1s-data we1s.mallet --keep-sequence --remove-stopwords`

Mac:
`bin/mallet import-dir --input we1s-data we1s.mallet --keep-sequence --remove-stopwords`

## 4. Train the Model
Now that we have created a MALLET format file, we can run a topic model. We do this using the `train-topics` command. There are many different parameters we can use to customize our model and model output; [these are listed in the MALLET Topic Modeling documentation](https://mimno.github.io/Mallet/topics){:target="_blank"}. We will discuss the components of this command during class on March 9.

Making sure you are still in the `mallet-2.0.8` folder, type the below command:

Windows:
`bin\mallet train-topics --input we1s.mallet --num-topics 25 --optimize-interval 10 --output-state we1s-topic-state.gz --output-topic-keys we1s-keys.txt --output-doc-topics we1s-composition.txt --word-topic-counts-file we1s-topic-counts.txt --diagnostics-file we1s-diagnostics.xml`

Mac:
`bin/mallet train-topics --input we1s.mallet --num-topics 25 --optimize-interval 10 --output-state we1s-topic-state.gz --output-topic-keys we1s-keys.txt --output-doc-topics we1s-composition.txt --word-topic-counts-file we1s-topic-counts.txt --diagnostics-file we1s-diagnostics.xml`

## 5. Examine the Model Outputs
We will look at each of these files together, but here is a list of the files we asked MALLET to produce for us (after the topic modeling process completes, you should find these in your `mallet-2.0.8` folder):

- State file (`we1s-topic-state.gz`): A compressed file containing every word in your corpus and each topic it contributes to.
- Topic keys file (`we1s-keys.txt`): A text file displaying the top words for each topic.
- Composition file (`we1s-composition.txt`): A text file indicating, by percentage, each topic that each document in your corpus contributes to.
- Topic counts file (`we1s-topic-counts.txt`): A text file indicating which topics each unique word in your corpus contributes to.
- Diagnostics file (`we1s-diagnostics.xml`): An xml file indicating a variety of diagnostics evaluating the overall fit and accuracy of your model. [Find out more about what these metrics are in the MALLET documentation](https://mallet.cs.umass.edu/diagnostics.php){:target="_blank"}.

# Topic Modeling with Voyant
You can also use Voyant to do topic modeling. Voyant uses the same kind of topic modeling that MALLET uses (written by the same person). Here's how to do topic modeling using Voyant:

1. Go to [voyant-tools.org](https://voyant-tools.org/){:target="_blank"} and upload the zip file containing our data for this tutorial. I have the best success with Voyant when using Chrome.
2. Once Voyant loads, go to the panel on the far right and select the window icon ("Click to choose another tool for this panel location..."). Select Document Tools > Topics. Voyant will then produce a topic model of the corpus. By default, this model will have 10 topics, and each topic will list the top 10 words associated with that topic. You can change the number of topics you want to model or the number of top words you want to display by using the "Topics" and "Terms" sliders at the bottom of this panel.
3. Voyant makes it slightly easier to visually explore your model results (though you have fewer options for customizing your model using Voyant). The topics are listed on the left side of the panel interface; each one is a different color. Clicking on a topic highlights the documents that contribute the most to that topic in the right side of the panel. You can also use the search bar at the bottom of the panel to search for a specific word among the top words in the model.
4. If you're using Chrome (tested only on a Chrome browser running on a Mac laptop): To read a specific article associated with a particular topic, right- or control-click on the document name in the "Documents" column of the Topics panel. Select the option to "Copy" the filename. Then, go down to the bottom left panel of the Voyant interface and select "Documents". Paste the filename you copied into the search bar at the bottom of this interface and press enter/return. The document filename should show up in the "Documents" panel. Click on it. Up in the top row of the Voyant interface, you will now see the contents of the file appear in the "Reader" panel. This allows you to read documents associated with particular topics.

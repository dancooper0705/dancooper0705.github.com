---
layout: post
title: "tensorflow-keras-datasets-imdb-print-data"
date:  2019-10-13 15:00:00  +0800
categories: [dev]
tags: [tensorflow, keras]
---

## what is tensorflow
A python package which implement neural network machine learning

## what is keras
A python package which runs marchin leanring. Its nerual network backend could be tensorflow.

## environment
macOS High Sierra
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
```

## python version
```bash
bash-3.2$ python3 --version
Python 3.7.3
```

## python module version
```bash
bash-3.2$ pip3 list
numpy                1.17.2
matplotlib           3.1.1
tensorflow           2.0.0
```

## source
```python
import tensorflow.keras as keras
import tensorflow.keras.datasets.imdb as imdb

train_x = None
train_y = None
test_x = None
test_y = None
id_to_word = None

def download_data():
    global train_x
    global train_y
    global test_x
    global test_y
    global id_to_word
    NUM_WORDS = 1000 # only use top 1000 words
    INDEX_FROM = 3   # word index offset
    (train_x, train_y),(test_x, test_y) = keras.datasets.imdb.load_data(num_words=NUM_WORDS, index_from=INDEX_FROM)
    word_to_id = keras.datasets.imdb.get_word_index()
    word_to_id = {k:(v+INDEX_FROM) for k,v in word_to_id.items()}
    word_to_id["<PAD>"] = 0
    word_to_id["<START>"] = 1
    word_to_id["<UNK>"] = 2
    word_to_id["<UNUSED>"] = 3
    id_to_word = {value:key for key,value in word_to_id.items()}

def print_train_data(n):
    for i in range(n):
        print('train_x[' + str(i) + ']: ' + ' '.join(id_to_word[id] for id in train_x[i] ))
        print('train_y[' + str(i) + ']: ' + str(train_y[i]))

def print_test_data(n):
    for i in range(n):
        print('test_x[' + str(i) + ']: ' + ' '.join(id_to_word[id] for id in test_x[i] ))
        print('test_y[' + str(i) + ']: ' + str(test_y[i]))

def main():
    download_data()
    print_train_data(5)
    print_test_data(5)

if __name__ == "__main__":
    main()
```

## output
```
print_train_data
train_x[0]: <START> this film was just brilliant casting <UNK> <UNK> story direction <UNK> really <UNK> the part they played and you could just imagine being there robert <UNK> is an amazing actor and now the same being director <UNK> father came from the same <UNK> <UNK> as myself so i loved the fact there was a real <UNK> with this film the <UNK> <UNK> throughout the film were great it was just brilliant so much that i <UNK> the film as soon as it was released for <UNK> and would recommend it to everyone to watch and the <UNK> <UNK> was amazing really <UNK> at the end it was so sad and you know what they say if you <UNK> at a film it must have been good and this definitely was also <UNK> to the two little <UNK> that played the <UNK> of <UNK> and paul they were just brilliant children are often left out of the <UNK> <UNK> i think because the stars that play them all <UNK> up are such a big <UNK> for the whole film but these children are amazing and should be <UNK> for what they have done don't you think the whole story was so <UNK> because it was true and was <UNK> life after all that was <UNK> with us all
train_y[0]: 1
train_x[1]: <START> big <UNK> big <UNK> bad music and a <UNK> <UNK> <UNK> these are the words to best <UNK> this terrible movie i love cheesy horror movies and i've seen <UNK> but this had got to be on of the worst ever made the plot is <UNK> <UNK> and ridiculous the acting is an <UNK> the script is completely <UNK> the best is the end <UNK> with the <UNK> and how he worked out who the killer is it's just so <UNK> <UNK> written the <UNK> are <UNK> and funny in <UNK> <UNK> the <UNK> is big lots of <UNK> <UNK> men <UNK> those cut <UNK> <UNK> that show off their <UNK> <UNK> that men actually <UNK> them and the music is just <UNK> <UNK> that plays over and over again in almost every scene there is <UNK> music <UNK> and <UNK> taking away <UNK> and the <UNK> still doesn't close for <UNK> all <UNK> <UNK> this is a truly bad film whose only <UNK> is to look back on the <UNK> that was the <UNK> and have a good old laugh at how bad everything was back then
train_y[1]: 0
train_x[2]: <START> this has to be one of the worst films of the <UNK> when my friends i were watching this film being the <UNK> audience it was <UNK> at we just <UNK> watched the first half an hour with our <UNK> <UNK> the <UNK> at how bad it really was the rest of the time everyone else in the <UNK> just started talking to each other <UNK> or <UNK> <UNK> into their <UNK> that they actually <UNK> money they had <UNK> working to watch this <UNK> <UNK> for a film it must have looked like a great idea on <UNK> but on film it looks like no one in the film has a <UNK> what is going on crap acting crap <UNK> i can't get across how <UNK> this is to watch save yourself an hour a bit of your life
train_y[2]: 0
train_x[3]: <START> the <UNK> <UNK> at <UNK> the <UNK> sort many years after the <UNK> i can still see in my <UNK> eye an <UNK> lady my <UNK> mother <UNK> the battle of <UNK> she makes the characters come <UNK> her <UNK> is that of an eye <UNK> one to the events on the <UNK> <UNK> a <UNK> or so from where she lives br br of course it happened many years before she was <UNK> but you wouldn't guess from the way she tells it the same story is told in <UNK> the <UNK> and <UNK> of <UNK> as i <UNK> it with a friend one night in <UNK> a local cut in to give his version the <UNK> <UNK> to <UNK> time br br stories <UNK> down like this become part of our being who doesn't remember the stories our parents told us when we were children they become our <UNK> world and as we <UNK> older they maybe still <UNK> as <UNK> or as an emotional <UNK> fact and <UNK> <UNK> with <UNK> role <UNK> <UNK> stories <UNK> <UNK> and mystery br br my name is <UNK> like my <UNK> and his <UNK> before him our <UNK> <UNK> himself to us and also <UNK> the story that <UNK> back through <UNK> it <UNK> stories within stories stories that <UNK> the <UNK> wonder of <UNK> its <UNK> <UNK> <UNK> in <UNK> the stuff of <UNK> yet <UNK> is <UNK> in reality this is what gives it its special <UNK> it has a <UNK> beauty and <UNK> <UNK> with some of the <UNK> <UNK> <UNK> you will ever hear br br <UNK> <UNK> <UNK> his <UNK> in <UNK> <UNK> before his death he <UNK> with <UNK> part of him <UNK> to be in the <UNK> first <UNK> to <UNK> out in <UNK> but he is <UNK> on the <UNK> <UNK> among a <UNK> <UNK> <UNK> br br yet there is a <UNK> <UNK> within him he <UNK> to know the truth the truth behind his <UNK> <UNK> stories where does <UNK> end and he wants to know the truth behind the death of his parents br br he is <UNK> to make a last <UNK> <UNK> to the <UNK> of one of <UNK> most <UNK> <UNK> can the truth be told or is it all in stories br br in this story about stories we <UNK> <UNK> <UNK> <UNK> <UNK> the <UNK> of old and the sometimes more <UNK> <UNK> of <UNK> truth in doing so we each <UNK> with <UNK> as he lives the story of his own life br br <UNK> the <UNK> <UNK> is probably the most <UNK> <UNK> and <UNK> beautiful film of <UNK> ever made like <UNK> i got <UNK> <UNK> with the <UNK> of <UNK> stories on more stories but also like <UNK> i <UNK> this once i saw the <UNK> picture ' forget the box <UNK> <UNK> of <UNK> and its like you might even <UNK> the <UNK> famous <UNK> of the <UNK> man to see a film that is true to <UNK> this one is probably unique if you maybe <UNK> on it <UNK> enough you might even re <UNK> the power of <UNK> and the age old question of whether there are some <UNK> that cannot be told but only <UNK>
train_y[3]: 1
train_x[4]: <START> worst <UNK> of my life br br i <UNK> this movie up at <UNK> for 5 because i <UNK> <UNK> it's <UNK> i can get some cheap laughs i was wrong completely wrong <UNK> way through the film all three of my friends were <UNK> and i was still <UNK> worst plot worst script worst movie i have ever seen i wanted to hit my head up against a <UNK> for an hour then i'd stop and you know why because it felt <UNK> good upon <UNK> my head in i <UNK> that <UNK> movie in the <UNK> and watched it <UNK> and that felt better than anything else i've ever done it took american <UNK> <UNK> of <UNK> and kill bill just to get over that crap i hate you <UNK> for actually going through with this and <UNK> a whole day of my life
train_y[4]: 0
print_test_data
test_x[0]: <START> please give this one a miss br br <UNK> <UNK> and the rest of the cast <UNK> terrible performances the show is <UNK> <UNK> <UNK> br br i don't know how michael <UNK> could have <UNK> this one on his <UNK> he almost seemed to know this wasn't going to work out and his performance was quite <UNK> so all you <UNK> fans give this a miss
test_y[0]: 0
test_x[1]: <START> this film <UNK> a lot of <UNK> because it <UNK> on <UNK> and character development the plot is very simple and many of the scenes take place on the same set in <UNK> <UNK> the <UNK> <UNK> character <UNK> but the film <UNK> to a <UNK> <UNK> br br the characters create an atmosphere <UNK> with sexual <UNK> and <UNK> <UNK> it's very interesting that robert <UNK> directed this <UNK> the style and <UNK> of his other films still the <UNK> <UNK> <UNK> style is <UNK> here and there i think what really makes this film work is the brilliant performance by <UNK> <UNK> it's definitely one of her <UNK> characters but she plays it so perfectly and <UNK> that it's scary michael <UNK> does a good job as the <UNK> young man <UNK> <UNK> <UNK> michael <UNK> has a small part the <UNK> <UNK> set <UNK> the <UNK> of the story very well in short this movie is a powerful <UNK> of <UNK> sexual <UNK> and <UNK> be <UNK> <UNK> up the atmosphere and pay attention to the <UNK> written script br br i <UNK> robert <UNK> this is one of his many films that <UNK> with <UNK> <UNK> subject matter this film is <UNK> but it's <UNK> and it's sure to <UNK> a strong emotional <UNK> from the viewer if you want to see an <UNK> film some might even say <UNK> this is worth the time br br unfortunately it's very difficult to find in video <UNK> you may have to buy it off the <UNK>
test_y[1]: 1
test_x[2]: <START> many animation <UNK> <UNK> <UNK> <UNK> the great <UNK> <UNK> of one special <UNK> of the art <UNK> animation which he <UNK> almost single <UNK> and as it happened almost <UNK> as a young man <UNK> was more interested in <UNK> than the cinema but his <UNK> attempt to film two <UNK> <UNK> fighting <UNK> to an <UNK> <UNK> in film making when he <UNK> he could <UNK> <UNK> by <UNK> <UNK> <UNK> and <UNK> them one <UNK> at a time this <UNK> <UNK> to the production of <UNK> <UNK> classic short the <UNK> <UNK> which he made in <UNK> in <UNK> at a time when <UNK> picture animation of all <UNK> was in its <UNK> br br the political <UNK> of the <UNK> <UNK> <UNK> <UNK> to move to <UNK> where one of his first <UNK> <UNK> was a dark political <UNK> <UNK> known as <UNK> or the <UNK> who wanted a king a <UNK> of black comedy can be found in almost all of films but here it is very dark indeed <UNK> more at <UNK> <UNK> who can <UNK> the <UNK> <UNK> than children who would most <UNK> find the <UNK> <UNK> i'm middle <UNK> and found it pretty <UNK> myself and indeed <UNK> of the film <UNK> for english <UNK> viewers of the <UNK> were given title <UNK> <UNK> with <UNK> and <UNK> in order to help <UNK> the <UNK> <UNK> of the <UNK> br br our tale is set in a <UNK> the <UNK> <UNK> where the <UNK> are <UNK> with their <UNK> and have called a special <UNK> to see what they can do to <UNK> <UNK> they <UNK> to <UNK> <UNK> for a king the <UNK> are <UNK> <UNK> in this opening sequence it couldn't have been easy to make so many <UNK> <UNK> look <UNK> <UNK> while <UNK> for his part is <UNK> as a <UNK> white <UNK> guy in the <UNK> who looks like <UNK> rather be taking a <UNK> when <UNK> <UNK> them a <UNK> like god who <UNK> them the <UNK> <UNK> that this is no <UNK> and <UNK> a different king <UNK> <UNK> <UNK> them a <UNK> br br <UNK> with this <UNK> looking new king who <UNK> above them the <UNK> <UNK> him with a <UNK> of <UNK> <UNK> <UNK> the <UNK> <UNK> forward to hand him the <UNK> to the <UNK> as <UNK> <UNK> <UNK> the <UNK> to <UNK> horror the <UNK> <UNK> <UNK> the <UNK> and then goes on a <UNK> <UNK> <UNK> <UNK> at <UNK> a title <UNK> <UNK> <UNK> <UNK> of the <UNK> <UNK> throughout the <UNK> when the now <UNK> <UNK> once more <UNK> <UNK> for help he <UNK> his <UNK> and <UNK> their <UNK> with <UNK> <UNK> the <UNK> of our story <UNK> by a <UNK> <UNK> just before he is <UNK> is let well enough alone br br <UNK> the time period when this <UNK> little film was made and <UNK> the fact that it was made by a <UNK> <UNK> at the <UNK> of that <UNK> <UNK> <UNK> war it would be easy to see this as a <UNK> about those events <UNK> may or may not have had <UNK> <UNK> in mind when he made <UNK> but whatever <UNK> his <UNK> of material the film <UNK> as a <UNK> tale of <UNK> <UNK> <UNK> could be the <UNK> <UNK> <UNK> <UNK> or <UNK> in the <UNK> or any country of any era that <UNK> its <UNK> down and is <UNK> by <UNK> it's a <UNK> film even a <UNK> one in its <UNK> way but its message is no joke
test_y[2]: 1
test_x[3]: <START> i <UNK> love this type of movie however this time i found myself <UNK> to <UNK> the screen since i can't do that i will just <UNK> about it this was absolutely <UNK> the things that happen with the dead kids are very cool but the <UNK> people are <UNK> <UNK> i am a <UNK> man pretty big and i can <UNK> myself well however i would not do half the stuff the little girl does in this movie also the mother in this movie is <UNK> with her children to the point of <UNK> i wish i wasn't so <UNK> about her and her <UNK> because i would have otherwise enjoyed the flick what a number she was take my <UNK> and fast forward through everything you see her do until the end also is anyone else getting <UNK> of watching movies that are filmed so dark <UNK> one can hardly see what is being filmed as an audience we are <UNK> involved with the <UNK> on the screen so then why the hell can't we have night <UNK>
test_y[3]: 0
test_x[4]: <START> like some other people <UNK> i'm a die hard <UNK> fan and i loved this game br br this game starts <UNK> boring but <UNK> me it's worth it as soon as you start your <UNK> the <UNK> are fun and <
```

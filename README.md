**Natural-language processing (NLP):**

Wikipedia says, Natural-language processing (NLP) is an area of computer science and artificial intelligence concerned with the interactions between computers and human (natural) languages, in particular how to program computers to fruitfully process large amounts of natural language data. Challenges in natural-language processing frequently involve speech recognition, natural-language understanding, and natural-language generation.


**NLP in iOS with NSLinguisticTagger:**

NSLinguisticTagger provides a uniform interface to a variety of natural language processing functionality with support for many different languages and scripts. One can use this class to segment natural language text into paragraphs , sentences, or words and tag information  about those segments such as parts of speech, lexical class, lemma, script and language.

**Part of speech (POS):**

In English language, noun, verb, adjective, adverb, pronoun , preposition , conjunction and interjection are part of speech.

Example :

```
import UIKit

let inputString = "In Old Delhi, a neighborhood dating to the 1600s, stands the imposing Mughal-era Red Fort, a symbol of India, and the sprawling Jama Masjid mosque, whose courtyard accommodates 25,000 people."


// tag schemes: tag schemes are constants that are used to identify pieces of information that we want from the input text. Tag schemes asks tagger to look for informations like
// Token type: a contant to classify each character as a word, punctuation or a whitespace
// Language: a constant to determine langugage of the token
// LexicalClass: this constant determines class of each token. i.e. it determines part of speech for a word, type of punctuation for a punctuation or type of whitespace for a whitespace
// Name type: this constant looks for tokens that are part of a named entity. It will look for a person's name , organizational name and name of a place
// Lemma: this constant returns the stem of word.
let tagger = NSLinguisticTagger(tagSchemes: [NSLinguisticTagScheme.tokenType, .language, .lexicalClass, .nameType, .lemma], options: 0)

// Options are the way to tell API as how to split the text. We are asking to ignore any punctuations and any whitespaces. Also, if there is a named entity then join it together i.e instead of considering "San" "Francisco" as two entities, join them together as one which is "San Francisco"
let options: NSLinguisticTagger.Options = [NSLinguisticTagger.Options.omitPunctuation, .omitWhitespace, .joinNames]

// Parts of Speech
func partOfSpeech() {
    tagger.string = inputString
    let range = NSRange(location: 0, length: inputString.utf16.count)
    
    tagger.enumerateTags(in: range, unit: NSLinguisticTaggerUnit.word, scheme: NSLinguisticTagScheme.lexicalClass, options: options) { (tag, tokenRange, _) in
        if let tag = tag {
            let word = (inputString as NSString).substring(with: tokenRange)
            print("\(tag.rawValue) -> \(word)")
        }
    }
}

partOfSpeech()```

**Lexical class:**

Lexical class is same as POS but may exclude parts of speech that are considered to be functional, like pronoun

**Identify Names:**

Names of person or places

**Perform Lemmatization:**

The process of grouping together the inflected forms of a word so that they can be analysed as a single item, identified by the word's lemma. Eg: go, goes, gone, went are lemma of go.

**Determine the language:**

Return the dominant language for the specified string

**Use cases for NSLinguisticTagger: **

1) Voice driven search - Parse and lemmatize the search command. Define grammar to map the spoken search command into an actual search query

2) To automatically create or suggest tags found in a document such as recongizing proper nouns, organisation names.

3) Facilitate conversational UI.



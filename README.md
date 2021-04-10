# PanScanner

PanScanner is a tool to make your personal cloud storage more secure using AI.
Personal cloud storage, such as Dropbox, Google Drive, and iCloud,  has brought various conveniences to people's lives, but also brought various privacy risks. Once hackers intrude into personal cloud storage accounts, a large number of privacy information will be leaked, such as taking private photos of sensitive parts, taking photos of important certificates, recording personal sensitive data files, etc. At the same time, intentional or unintentional anonymous sharing can easily lead to sensitive data being obtained by malicious individuals or organizations.
Our PanScanner uses AI technology to protect the privacy and security of personal cloud storage, as follows:

 - Using the object detection model to detect the sensitive credentials in personal cloud storage, and automatically mosaic the credentials in the images according to the needs.

- Using computer vision model to recognize the pictures of sensitive parts of the body in personal cloud storage, and automatically mosaic the pictures according to the needs.

- Using expert rules and NLP model to detect the sensitive personal information such as ID number, personal biometric information, address, contact person in the personal cloud storage, and automatically desensitize sensitive fields according to needs.

- Using the weak supervision algorithm, based on the existing noisy and imperfect expert rules, quickly obtain a large number of sensitive or insensitive training data, so as to further train a strong text classifier, improve the ability of automatically discovering sensitive data in personal cloud storage.

# Tool Details

It is easy to use our tool.

 usage: panscanner.py [-h] [-d DIR]

 optional arguments:
   -h, --help         show this help message and exit
   -d DIR, --dir DIR  Directory to scan


1. Introduce the privacy and security issues of personal cloud storage.

Personal cloud storage, such as Dropbox, Google Drive, and iCloud,  has brought various conveniences to people's lives, but also brought various privacy risks. Once hackers intrude into personal cloud storage accounts, a large number of privacy information will be leaked, such as taking private photos of sensitive parts, taking photos of important certificates, recording personal sensitive data files, etc.  In 2018, Mikaela Hoover, an actress who starred in the movie Galaxy escort and played Nova's top commander's assistant, was hacked into her icloud account recently, revealing up to 40000 photos. Among them, 119 are Mikaela's personal privacy pictures. What's more, the hackers also published these pictures on Fappening.

2. How to use the object detection model to detect the sensitive credentials in personal cloud storage, and automatically mosaic the credentials in the images according to the needs.

People often take photos of sensitive personal information, such as ID card, bank card, driver's license, etc., intentionally or unintentionally, and store them in personal cloud storage. For example, you take an ID card with your Apple phone, and the phone syncs the photo to icloud automatically. If you're a very cautious person, maybe you can check your icloud regularly for sensitive photos. But it is a difficult task for most people, which is boring and hard to persist in.

Inspired by the unmanned vehicle, the unmanned vehicle uses the object detection model to automatically detect and identify vehicles and traffic lights from the video stream. So we thought of using object detection model to automatically detect sensitive pictures from thousands of photos. At present, there is no model that can be used directly, so we first collected thousands of typical sensitive pictures as training data, and then chose FCOS (Fully Convolutional One-Stage Object Detection) with leading performance to train on our dataset. 

When detecting sensitive images, we first use FCOS to filter, and then in order to further improve the accuracy, we use OCR (Optical Character Recognition) model to extract text information for comparison. FCOS model can return the coordinates of sensitive documents in the image, so we can directly mosaic the sensitive documents through opencv as needed.

3. How to use computer vision model to recognize the pictures of sensitive parts of the body in personal cloud storage, and automatically mosaic the pictures according to the needs.

Taking photos of sensitive parts of a person's body, once stolen by hackers, can easily become a bargaining chip for blackmail. We use Open NSFW (Not Safe/Suitable For Work) model to directly screen out suspected pornographic images. In order to improve the accuracy, we use the face comparison model FaceNet (A Unified Embedding for Face Recognition and Clustering https://arxiv.org/abs/1503.03832) to further screen out the pictures of the designated person (such as the user himself and his relatives and friends). We can delete these pictures as needed.

4. How to use expert rules and NLP model to detect the sensitive personal information such as ID number, personal biometric information, address, contact person in the personal cloud storage, and automatically desensitize sensitive fields according to needs.

Pdf, CSV, word and other files containing sensitive information such as ID card, mobile phone number, bank card number and communication address are often the targets of hackers. By collecting these information, hackers can directly cash in the black market, or further carry out targeted cyber crime. For the detection of these sensitive information, expert rules can be used. For example, structured information such as ID card, mobile phone number, bank card number can be detected by regular expression, and information such as communication address can be detected by natural language model tool such as NLTK(Natural Language Toolkit), Hanlp (Han Language Processing), and Spacy (Industrial-Strength Natural Language Processing).  We can automatically desensitize sensitive fields according to needs.

5. How to use the weak supervision algorithm, based on the existing noisy and imperfect expert rules, quickly obtain a large number of sensitive or insensitive training data, so as to further train a strong text classifier, improve the ability of automatically discovering sensitive data in personal cloud storage.

The advantage of expert rules is that they can be interpreted well, but it is difficult to weigh the accuracy and recall rate of the data that we have not seen before. A natural idea is to train a text classification model to detect sensitive fields in documents. But collecting enough labeled training data is a very challenging task. If we directly use expert rules to label the collected unlabeled data, we will introduce a lot of noisy and classification conflict markers. So we use weak supervised learning to label training data quickly, and solve the problem of noise and classification conflict between expert rules at the same time. Here, our expert rules are accumulated before use, and Snorkel (a system for quickly generating training data with weak supervision) is used for weak supervision learning. We write Labeling Functions, combine Labeling Function Outputs with the Label Model, and training a classifier. We use a typical text classifier, TextCNN or BERT (Bidirectional Encoder Representation from Transformers).


6. Full text summary.

We introduced how to use AI technology to protect personal privacy of personal cloud storage. Our code will be open source later. It is highly recommended to use our tools to scan personal data before synchronizing it with personal cloud storage.

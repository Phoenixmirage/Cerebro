﻿# Cerebro
Το Cerebro είναι μία εφαρμογή που αναπτύχθηκε στα πλαίσια του μαθήματος Ανάπτυξη Λογισμικού για Δίκτυα και Τηλεπικοινωνίες. Σκοπός είναι η απομακρυσμένη διαχείριση συσκευών μέσω σημάτων που παράγονται από τον ανθρώπινο εγκέφαλο χρησιμοποιώντας δεδομένα που συλλέχθηκαν με τη χρήση του φορητού εγκεφαλογραφήματος Emotiv EPOC++.

## Android app :iphone:
Η Android εφαρμογή Cerebro αποτελείται από μία Main Activity που περιέχει κουμπιά on/off για την ενεργοποίηση του φακού και της ηχητικής ειδοποίησης, καθώς και ένα μενού που περιέχει επιλογές για: παραμετροποίηση της IP και του port μέσω των οποίων μπορεί να επικοινωνήσει με τον broker, παραμετροποίηση της συχνότητας με την οποία λαμβάνει εντολές και τέλος επιλογή εξόδου.

Έπειτα από την εισαγωγή των IP και port δημιουργεί ένα αντικείμενο της κλάσης MqttClient προκειμένου να πραγματοποιήσει αμφίδρομη επικοινωνία με το java app. Πιο συγκεκριμένα δέχεται εντολές τύπου on/off και στέλνει την συχνότητα με την οποία επιθυμεί να λαμβάνει τις εντολές αυτές.

// εισαγωγή επεξήγησης για background check σύνδεσης στο internet

## Java app :computer:
Η java εφαρμογή αποτελείται από ένα αρχείο που υπολογίζει την εντροπία των δεδομένων το οποίο και περιέχει την main της εφαρμογής, το αρχείο ProbabilityState που μας δίνεται, το αρχείο ΚΝΝalgorithm το οποίο υλοποιεί τον αλγόριθμο Knn και στέλνει τα αποτελέσματα στον buffer, τα αρχεία Consumer και Producer που περιέχουν τα συγχρονισμένα thread και τον buffer και τέλος το αρχείο MQTTclient που περιέχει τον client και τα απαραίτητα για την υλοποίηση του.

Ξεκινάμε την εφαρμογή τρέχοντας την Entropy.java, η οποία στέλνει και δέχεται δεδομένα απο την ProbabilityState και δημιουργεί μια κλάση KNNalgorithm, στην οποία αρχικοποιούμε τον MQTTclient και τους producer, consumer.

Από τα δεδομένα αφαιρούμε εκείνα των οποίων οι αισθητήρες είχαν QoS κάτω απο 4, έτσι πετυχαίνουμε efficiency 73.4% με κ=7.

Όταν όλα τα δεδομένα έχουν σταλθεί στον buffer μέσω της ΚΝΝ στέλνουμε ένα τελικό μήνυμα στον buffer "finish", το οποίο όταν σταλθεί στον client κάνει disconnect.


## Επικοινωνία :speech_balloon:
Για την επικοινωνία μεταξύ των δύο εφαρμογών έχουν χρησιμοποιηθεί οι αντίστοιχες Java και Android βιβλιοθήκες του MQTT, καθώς και ο mosquitto broker. Δημιουργούνται 2 topics, το commands στο οποίο είναι publisher η java εφαρμογή και το frequency στο οποίο κάνει publish η android εφαρμογή.

## Εκτέλεση :sound:
Έχοντας ήδη ανοιχτό τον mosquitto broker, ανοίγουμε πρώτα την android εφαρμογή και φροντίζουμε το κινητό μας να είναι συνδεδεμένο στο ίδιο δίκτυο με τον υπολογιστή όπου θα εκτελεστεί η java εφαρμογή. Στη συνέχεια εισάγουμε μέσω της κατάλληλης επιλογής του μενού την IP και port 1883. Έτσι η εφαρμογή εγγράφεται ως subscriber στο topic commands.
Έπειτα εκτελούμε την java εφαρμογή, η οποία τώρα θα μπορεί να κάνει pubish στο topic commands τα αντίστοιχα μηνύματα για τις on/off εντολές, ενώ παράλληλα εγγράφεται και ως subcriber στο topic frequency. Έτσι η android εφαρμογή θα μπορεί πλέον να κάνει και publish τα αντίστοιχα μηνύματα για την αλλαγή της συχνότητας αποστολής των on/off εντολών.

## Δημιουργοί :busts_in_silhouette:
Αδαμοπούλου Δέσποινα
Μπόκος Δημήτρης
Παπαχρήστου Άννα

## Σημειώσεις - μην ξεχάσουμε
1. gradle και στα δυο
2. τι χρησιμοποιήθηκε (intellij, android studio, paho κλπ)
3. ενδεικτικός κώδικας/εικόνες εκτέλεσης



namespace ShiftVerschluesselung
{
    internal class Program
    {
        // Die Main-Methode ist der Einstiegspunkt des Programms
        static void Main(string[] args)
        {
            // Der verschlüsselte Text, den wir entschlüsseln wollen
            string encryptedText = "IZW WOZNCCM FSWHLJX UILR SMHGT WVZXH! DYE DQEVG PMHN HCO NLE TSBUZFLUHA GYGR NKW MMTLV!";

            // Schleife zur Ausprobierung aller möglichen Verschiebungen von 1 bis 25
            // Die Verschiebung 0 würde den Text nicht verändern, daher starten wir bei 1
            for (int startShift = 1; startShift < 26; startShift++)
            {
                // Entschlüsselt den verschlüsselten Text mit der aktuellen Verschiebung
                string decryptedText = DecryptShiftCipher(encryptedText, startShift);

                // Gibt die aktuelle Verschiebung und den entschlüsselten Text auf der Konsole aus
                // Diese Ausgabe hilft zu sehen, wie der Text bei jeder Verschiebung aussieht
                Console.WriteLine($"Shift {startShift}: {decryptedText}");
            }
        }

        // Methode zur Entschlüsselung des Textes mit einer bestimmten Verschiebung
        // Diese Methode implementiert den Caesar-Chiffre-Algorithmus zur Entschlüsselung
        static string DecryptShiftCipher(string input, int startShift)
        {
            // Wandelt den Eingabetext in ein Array von Zeichen um, um Zeichen einzeln bearbeiten zu können
            char[] buffer = input.ToCharArray();

            // Setzt die Anfangsverschiebung auf den übergebenen Wert
            int shift = startShift;

            // Schleife, um jedes Zeichen im Array zu verarbeiten
            for (int i = 0; i < buffer.Length; i++)
            {
                // Holt das aktuelle Zeichen aus dem Array
                char letter = buffer[i];

                // Überprüft, ob das Zeichen ein Buchstabe ist
                // Zahlen, Leerzeichen und Sonderzeichen werden nicht verändert
                if (char.IsLetter(letter))
                {
                    // Bestimmt den Basisbuchstaben ('A' für Großbuchstaben oder 'a' für Kleinbuchstaben)
                    char offset = char.IsUpper(letter) ? 'A' : 'a';

                    // Entschlüsselt den Buchstaben durch Subtrahieren der Verschiebung
                    letter = (char)(letter - shift);

                    // Falls der Buchstabe vor 'A' oder 'a' im Alphabet fällt, muss er um 26 Stellen zurückrollen
                    // Dies stellt sicher, dass wir im Bereich der Buchstaben bleiben (Wrap-around)
                    while (letter < offset)
                    {
                        letter = (char)(letter + 26);
                    }

                    // Setzt das entschlüsselte Zeichen an die richtige Stelle im Array ein
                    buffer[i] = letter;

                    // Erhöht die Verschiebung für den nächsten Buchstaben
                    // Diese Zeile wird verwendet, um den Algorithmus mit variabler Verschiebung zu testen
                    // Allerdings könnte diese Erhöhung in der aktuellen Implementierung redundant sein
                    shift++;
                }
            }
            // Wandelt das Zeichen-Array zurück in einen String und gibt ihn zurück
            // Dies ist der entschlüsselte Text für die gegebene Verschiebung
            return new string(buffer);
        }
    }
}

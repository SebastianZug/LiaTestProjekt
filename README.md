<!--

author:   Sebastian Zug
email:    sebastian.zug@informatik.tu-freiberg.de
version:  0.0.1
language: de
narrator: Deutsch Female

import: https://raw.githubusercontent.com/liaScript/rextester_template/master/README.md

@run: @Rextester.C_clang

@run_stdin: @Rextester.C_clang(false,`@input(1)`)
-->

# Meine LiaScript Experimentierdatei
** TU Bergakademie Freiberg 2019**

Link auf dieses Dokument im Versionsmanagementsystem GitHub

[https://github.com/SebastianZug/LiaTestProjekt](https://github.com/SebastianZug/LiaTestProjekt)

Die interaktive Form ist unter diese Link zu finden ->
[LiaScript Test](https://liascript.github.io/course/?https://raw.githubusercontent.com/SebastianZug/LiaTestProjekt/master/README.md#1)

---------------------------------------------------------------------

Beispiel von [https://de.wikipedia.org/wiki/Integrierter_Assembler](https://de.wikipedia.org/wiki/Integrierter_Assembler)

```c    HelloWorld.c
#include <stdio.h>

int main(void)
{
  int foo = 5;
  int bar = 4;

  /* Hier beginnt der Inline-Assembler Abschnitt in AT&T-Syntax */
  __asm__ (
      "add %1, %0\n\t" /* Addiert den Wert von Operand %1 zum Wert von Operand %0. */
      "inc %0"         /* Erhöht den Wert von Operand %0 um 1. */

      /* Definition der Nebenbedingungen:
       * Diese weisen den C-Variablen der Reihe nach aufzählend einen für den Inline-Assemblercode nutzbaren Operanden
       * zu und teilen dem Compiler mit, auf welche Weise (lesend und/oder schreibend) dieser im Inline-Assemblercode
       * verwendet werden kann und auf welche Register dieser beschränkt ist. Dadurch wird eine korrekte und effiziente
       * Übergabe der Variablenwerte in und aus dem Assemblercodeabschnitt gewährleistet. */
      : "+r" (bar) /* Gibt an, dass die Variable bar sowohl gelesen als auch beschrieben ('+') wird und deren Wert in
                    * ein allgemeines Register ('r') zu platzieren ist.
                    * Als erster Operand wird er im Assemblercodeabschnitt unter der Bezeichnung %0 genutzt. */
      : "g" (foo)  /* Beschränkt die Verwendung der Variable foo nur zum Lesen. Sie kann auf beliebige Weise ('g', im
                    * Speicher, in einem Register oder als Direktwert) an den Assemblerteil übergeben werden.
                    * Als zweiter Operand wird er im Assemblercodeabschnitt unter der Bezeichnung %1 genutzt */
      : "cc"       /* Gibt an, dass die Statusanzeige (durch die Befehle add und inc) verändert wurde. */
  );

  /* Hier geht's mit C Code weiter. */
  printf("Ergebnis: %i\n", bar);
  return 0;
}
```
@run

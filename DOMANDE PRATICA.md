**DOMANDE PRATICA**


**1. Chiudere le issue in automatico su github tramite commit**
	

git commit -m "Fixes #NumeroIssue"

La parola chiave utilizzata "Fixes" è una closing keyword riconosciut da github
Significa circa questo commit risolve/chiude la issue #NumeroIssue

**------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------**

**2. Comandi git**
	
	git add .
	git commit -m "messaggio"
	git push
	git pull


**------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------**


**3. Github action, come funziona per la build automation e continuous integration**

Github actions è il **sistema di automazione** integrato di github che permette di **definire dei workflow** (in file **YAML** nella cartella **.github/workflows**) eseguiti 
automaticamente in **risposta** **a** **eventi** come push o pull\_request

Nel contesto della **BUILD AUTOMATION**, il workflow esegue automaticamente il **processo di build**, **scarica le dipendenze** (es con maven), **compila il progetto**, **esegue i test** e **produce artefatti**

Nel contesto della **CONTINUOUS INTEGRATION**, ogni **modifica integrata nel repository** viene verificata automaticamente tramite la **pipeline**, 
così da **individuare** rapidamente **errori di compilazione** o **test falliti** e mantenere la **main branch sempre stabile**


**-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------**


**4. DESCRIVERE COM'è POSSIBILE CON MAVEN:**

* **Creare un progetto a partire da un template.**
* **Gestire il codice sorgente e il codice dei test di unità.**
* **Gestire le librerie di produzione e le librerie di test.**
* **Configurare uno strumento che dev'essere eseguito in una fase del processo di build**
  **(per es Esecuzione del code coverage o dell'analisi statica del codice con checkstyle)**


Con Maven il processo di build viene configurato tramite il file `pom.xml` e segue una struttura standard del progetto. 
Un progetto può essere creato da un template tramite gli archetype, ad esempio con `mvn archetype:generate`. 
Il codice sorgente viene posto in `src/main/java`, mentre il codice dei test di unità viene posto in `src/test/java`.

Le librerie vengono gestite dichiarando le dipendenze nel `pom.xml`. 
Ad esempio, JUnit può essere dichiarato come dipendenza di test:

<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>

Lo scope `test` indica che la libreria è necessaria solo per compilare ed eseguire i test, e non per il codice di produzione.


Maven permette anche di configurare strumenti da eseguire durante la build tramite plugin. 
Ad esempio, Checkstyle può essere associato alla fase `verify` del lifecycle:

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-checkstyle-plugin</artifactId>
            <version>3.3.1</version>
            <executions>
                <execution>
                    <phase>verify</phase>
                    <goals>
                        <goal>check</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>

In questo modo Maven gestisce automaticamente struttura del progetto, dipendenze, librerie di test e strumenti aggiuntivi da eseguire nelle varie fasi del processo di build.


**---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------**


**5. Un framework di test di unità deve avere le seguenti funzionalità:**

* **Un modo per configurare l'ambiente di esecuzione del test.**
* **Un modo per selezionare un test o un insieme di test da eseguire.**
* **Un modo per analizzare i valori aspettati, prodotti dalle unità.**
* **Un modo standard per eseguire ed esprimere se il test è stato superato, se è fallito o se sono**
  **stati prodotti degli errori.**

**Descrivere come sono implementate nel framework JUnit.**


In JUnit le funzionalità di un framework per test di unità sono implementate tramite **annotazioni**, **asserzioni** e **runner**.

La **configurazione dell’ambiente di test** avviene tramite metodi di **setup** e **teardown**, annotati ad esempio con '**@Before**' e '**@After**', 
che permettono di **preparare e ripulire** l’ambiente **prima e dopo ogni test**.

La **selezione dei test** avviene tramite **l’annotazione** '**@Test**', che identifica i metodi da eseguire come test. 
I test possono poi essere eseguiti **singolarmente**, **per classe**, **per suite** o **tramite strumenti di build come Maven**.

Il **confronto tra valori attesi e valori prodotti** dall’unità testata avviene **tramite le asserzioni**, 
come `**assertEquals**`, `**assertTrue**`, `**assertFalse**` o `**assertThrows**`.

Infine, JUnit fornisce un **modo standard per eseguire i test e riportarne l’esito**: 
un test è superato se tutte le asserzioni sono soddisfatte, fallisce se un’asserzione non è verificata, 
oppure produce errore se viene sollevata un’eccezione non prevista.


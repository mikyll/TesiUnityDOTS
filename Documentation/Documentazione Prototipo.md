# Documentazione Prototipo (ITA)

Il prototipo consiste in un piccolo gioco multigiocatore in cui ogni giocatore muove il proprio personaggio 
capsula e può interagire con i vari oggetti di scena. È stato realizzato interamente con i package forniti 
da DOTS.
<br/>
<p align="center">
	<a href="./Prototype%20Documentation.md">English <kbd><img width="20px" src="https://flagicons.lipis.dev/flags/4x3/gb.svg"></kbd></a>
	·
	<a href="/README.it.md">Home page</a>
</p>

<!-- TABLE OF CONTENTS -->
<details open="open">
	<summary><h2 style="display: inline-block">Indice</h2></summary>
	<ol>
		<li><a href="#obbiettivo-prototipo">Obbiettivo Prototipo</a></li>
		<li><a href="#principali-funzionalità">Principali Funzionalità</a></li>
		<li><a href="#build-applicazione-standalone">Build Applicazione Standalone</a></li>
		<li><a href="#flusso-di-esecuzione">Flusso di Esecuzione</a></li>
		<li><a href="#codice">Codice</a>
			<ul>
				<li><a href="#connessioni">Connessioni</a></li>
				<li><a href="#input">Input</a></li>
				<li><a href="#movimento">Movimento</a></li>
				<li><a href="#visuale-in-terza-persona">Visuale in Terza Persona</a></li>
				<li><a href="#portali-cambia-colore">Portali Cambia-Colore</a></li>
				<li><a href="#teletrasporto">Teletrasporto</a></li>
				<li><a href="#spawn-di-entità">Spawn di Entità</a></li>
				<li><a href="#raccolta-di-entità">Raccolta di Entità</a></li>
			</ul>
		</li>
		<li><a href="#riferimenti-utili">Riferimenti Utili</a>
			<ul><a href="#documentazione">Documentazione</a></ul>
			<ul><a href="#repository-github">Repository GitHub</a></ul>
			<ul><a href="#forum-dots">Forum DOTS</a></ul>
		</li>
	</ol>
</details>

## Obbiettivo Prototipo

L'obbiettivo del prototipo è quello di realizzare un gameplay basilare, con movimento dei personaggi e 
piccole interazioni con l'ambiente di gioco, sfruttando i package forniti dall'architettura Unity DOTS. 
In particolare, sono stati utilizzati i seguenti package:
* Entities, per realizzare il modello basato su Entità, Componenti e Sistemi (ECS).
* NetCode, per realizzare la parte legata al networking, ovvero le connessioni dei giocatori (client) al 
server di gioco e la comunicazione fra questi.
* Physics, per realizzare le meccaniche legate alla fisica (entità statiche/dinamiche, sistema delle 
collisioni, ecc.).


## Principali Funzionalità

<table>
	<tr>
		<td><b>Funzionalità</b></td>
		<td><b>File</b></td>
		<td width="40%"><b>Dimostrazione</b></td>
	</tr>
	<tr>
		<td>Accumulo degli input e movimento personaggio capsula</td>
		<td><a href="/DOTS%20Prototype/Assets/Scripts/Components/PlayerMovementSpeed.cs">PlayerMovementSpeed</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Systems/PlayerInputSystem.cs">PlayerInputSystem.cs</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Systems/PlayerMovementSystem.cs">PlayerMovementSystem.cs</a></td>
		<td width="40%"><img src="/Documentation/Images/GIF_Movement.gif" alt="MovimentoGIF"/></td>
	</tr>
	<tr>
		<td>Camera follow in terza persona</td>
		<td><a href="/DOTS%20Prototype/Assets/Scripts/Components/PlayerCameraFollowComponent.cs">PlayerCameraFollowComponent.cs</a><br/>
			<a href="/DOTS%20Prototype/Assets/Scripts/Systems/CameraFollowSystem.cs">CameraFollowSystem.cs</a></td>
		<td width="40%"><img src="/Documentation/Images/GIF_CameraFollow.gif" alt="CameraFollowGIF"/></td>
	</tr>
	<tr>
		<td>Portali cambia-colore</td>
		<td><a href="/DOTS%20Prototype/Assets/Scripts/Components/PersistentChangeMaterialOnTriggerComponent.cs">PersistentChangeMaterialOnTriggerComponent.cs</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Systems/PersistentChangeMaterialOnTriggerSystem.cs">PersistentChangeMaterialOnTriggerSystem.cs</a><br/><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Components/TemporaryChangeMaterialOnTriggerComponent.cs">TemporaryChangeMaterialOnTriggerComponent.cs</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Systems/TemporaryChangeMaterialOnTriggerSystem.cs">TemporaryChangeMaterialOnTriggerSystem.cs</a></td>
		<td width="40%"><img src="/Documentation/Images/GIF_ChangeMaterialPortals.gif" alt="PortaliColoreGIF"/></td>
	</tr>
	<tr>
		<td>Teletrasporti</td>
		<td><a href="/DOTS%20Prototype/Assets/Scripts/Components/TeleportComponent.cs">TeleportComponent.cs</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Systems/TeleportSystem.cs">TeleportSystem.cs</a></td>
		<td width="40%"><img src="/Documentation/Images/GIF_Teleport.gif" alt="TeletrasportoGIF"/></td>
	</tr>
	<tr>
		<td>Spawn entità in punti randomici di un volume</td>
		<td><a href="/DOTS%20Prototype/Assets/Scripts/Components/SpawnRandomObjectsAuthoring.cs">SpawnRandomObjectsAuthoring.cs</a></td>
		<td width="40%"><img src="/Documentation/Images/InspectorSpawnRandomAuthoring.png" alt="SpawnRandomAuthoring" width="60%"/>
			<img src="/Documentation/Images/GIF_SpawnEntities.gif" alt="SpawnEntitiesGIF" width="35%"/></td>
	</tr>
	<tr>
		<td>Raccolta oggetti "collectibles"</td>
		<td><a href="/DOTS%20Prototype/Assets/Scripts/Components/PlayerScoreComponent.cs">PlayerScoreComponent</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Components/PickUpSystem.cs">CollectibleTagComponent.cs</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Components/DeleteTagComponent.cs">DeleteTagComponent.cs</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Systems/PickUpSystem.cs">PickUpSystem.cs</a><br/>
		<a href="/DOTS%20Prototype/Assets/Scripts/Systems/DeleteCollectibleSystem.cs">DeleteCollectibleSystem.cs</a></td>
		<td width="40%"><img src="/Documentation/Images/GIF_PickupCollectibles.gif" alt="CollectiblesGIF"/></td>
	</tr>
</table>


## Build Applicazione Standalone
Per eseguire la <a href="https://docs.unity3d.com/Packages/com.unity.entities@0.17/manual/install_setup.html#standalone-builds">build</a> di un'applicazione Unity realizzata usando DOTS, è necessario utilizzare i package Platforms (com.unity.platforms.\*). In particolare, nel caso di un'<a href="https://docs.unity3d.com/Packages/com.unity.netcode@0.6/manual/client-server-worlds.html#standalone-builds">applicazione multiplayer</a>, NetCode utilizza la proprietà <i>Server Build</i> in Build Settings e gli scripting define symbols in **Project Settings** > **Player** per capire che tipo di applicazione buildare (solo client, solo server o scelta a runtime).
### Esempio Windows
1. Controllare che il package com.unity.platforms.windows sia presente nel PackageManager.
2. Creare una Configurazione di Build: **Project Window** > **Create** > **Build** > **Windows Classic Build Configuration**.
3. Selezionare la configurazione ed eseguire la build.
<p float="left">
<img src="/Documentation/Images/WindowsBuild%20(1).png" alt="WindowsBuild (1)" width="50%"/>
<img src="/Documentation/Images/WindowsBuild%20(2).png" alt="WindowsBuild (2)" width="45%"/>
</p>

## Flusso di Esecuzione

Il flusso di esecuzione del prototipo è il seguente:
1. All'avvio dell'applicazione viene eseguito il sistema Game, contenuto in Game.cs. Questo sistema realizza
	la connessione dei client al server, differenziando l'esecuzione del server, il quale si mette in ascolto
	per le connessioni, da quella dei client, che si connettono al server.
2. I client eseguono il sistema GoInGameClientSystem, che invia una richiesta al server per entrare in gioco
	e iniziare a inviare comandi e ricevere snapshot (ovvero gli aggiornamenti dello stato di gioco).
3. Il server esegue il sistema GoInGameServerSystem, che riceve le richieste di entrare in gioco e per
	ciascun giocatore abilita la comunicazione tramite comandi e snapshot, e genera un personaggio capsula.
4. L'applicazione, tramite il sistema PlayerInputSystem, controlla continuamente se il giocatore immette input 
	da tastiera e in caso li accumula in un buffer e li invia al server.
6. Il sistema PlayerMovementSystem applica gli input alle varie capsule, utilizzando la predizione lato client
	per rendere l'esecuzione più fluida e far percepire il meno possibile la latenza della rete.
8. Nel mentre si aggiornano anche gli altri sistemi che realizzano le varie funzionalità.


## Codice

NB: i pezzi di codice mostrati sono stati ritagliati per mostrare solo le parti fondamentali spiegate
nel testo.

### Connessioni
<details>
Il file <a href="/DOTS%20Prototype/Assets/Scripts/Game.cs">Game.cs</a> 
contiene la <i>logica per realizzare la connessione</i>. In particolare al suo interno c'è un sistema 
<b>Game</b> che controlla se il codice che esegue è quello di un client o di un server, svolgendo 
rispettivamente connect o listen.<br/>
Una volta che client e server sono connessi, è necessario indicare a NetCode che i client sono pronti a 
inviare comandi e ricevere snapshot dal server: appena la connessione viene stabilita, lato client inizia ad 
eseguire il sistema <b>GoInGameClientSystem</b>, che invia una RPC al server; lato server inizia ad eseguire il 
sistema <b>GoInGameServerSystem</b> che riceve la RPC e marchia il client come "in gioco", aggiungendo il 
componente <b>NetworkStreamInGame</b> all'entità che rappresenta la connessione e creando una personaggio 
capsula per il giocatore corrispondente al client.

#### Componente `EnableGame`

Dichiariamo la struttura <b>EnableGame</b> che ci servirà più avanti per indicare che i client o il server sono
pronti a stabilire la connessione ed entrare in gioco.

#### Sistema `Game`

[UpdateInWorld(UpdateInWorld.TargetWorld.Default)] indica che il sistema Game dev'essere eseguito nel mondo 
di default, in quanto questo mondo è sempre presente perché istanziato automaticamente da Unity.

Poiché il codice del sistema Game realizza la connessione, dev'essere eseguito una sola volta per run
dell'applicazione. Dunque, utilizziamo un ulteriore singleton <b>InitGameComponent</b>, per indicare quando il 
codice di questo sistema è già stato eseguito una volta: nella OnCreate() usiamo il metodo 
<b>RequireSingletonForUpdate<>()</b> per indicare l'entità che dev'essere presente affinché OnUpdate() venga
chiamata; dopodiché creiamo l'entità avente questo componente; infine nella OnUpdate() rimuoviamo tale
entità, così Unity non chiama più OnUpdate() del sistema Game.

```csharp
protected override void OnCreate()
{
	RequireSingletonForUpdate<InitGameComponent>();
	EntityManager.CreateEntity(typeof(InitGameComponent));
}
```

La OnUpdate() itera su tutti i mondi presenti nell'applicazione e, dopo aver ottenuto il sistema
<b>NetworkStreamReceiveSystem</b> (che espone i metodi Connect e Listen), controlliamo se ci troviamo in un
client o in un server:
* Nel caso l'applicazione sia un client, sarà presente il mondo ClientWorld, al cui interno vi sarà il
gruppo di sistemi <b>ClientSimulationSystemGroup</b>. Dunque creiamo l'entità singleton <b>EnableGame</b> e
facciamo una connect a localhost:7979.
* Nel caso l'applicazione sia un server, sarà presente il mondo ServerWorld, al cui interno vi sarà il
gruppo di sistemi <b>ServerSimulationSystemGroup</b>. Dunque creiamo l'entità singleton <b>EnableGame</b> e
facciamo una listen sulla porta 7979.
```csharp
protected override void OnUpdate()
{
    EntityManager.DestroyEntity(GetSingletonEntity<InitGameComponent>());
    foreach (var world in World.All)
    {
        var network = world.GetExistingSystem<NetworkStreamReceiveSystem>();
        if (world.GetExistingSystem<ClientSimulationSystemGroup>() != null)
        {
            world.EntityManager.CreateEntity(typeof(EnableGame));
            NetworkEndPoint ep = NetworkEndPoint.LoopbackIpv4;
            ep.Port = 7979;
            ep = NetworkEndPoint.Parse(ClientServerBootstrap.RequestedAutoConnect, 7979);

            network.Connect(ep);
        }
        else if (world.GetExistingSystem<ServerSimulationSystemGroup>() != null)
        {
            world.EntityManager.CreateEntity(typeof(EnableGame));
            NetworkEndPoint ep = NetworkEndPoint.AnyIpv4;
            ep.Port = 7979;

            network.Listen(ep);
        }
    }
}
```

#### Componente `GoInGameRequest`

Poiché non è stato aggiunto il componente <b>NetworkStreamInGame</b> all'entità che rappresenta la connessione 
fra un client ed il server, questi non possono comunicare inviando comandi o snapshot. Quindi, utilizziamo 
una RPC NetCode (IRpcCommand) per notificare al server che il client è pronto ad entrare in gioco, così il 
server può marcare la connessione e avviare la comunicazione.<br/>
Come spiegato nella documentazione di <a href="https://docs.unity3d.com/Packages/com.unity.netcode@0.6/manual/rpcs.html">NetCode</a>, 
per inviare una RPC è necessario creare un entità ed aggiungervi il comando RPC creato ed il componente
SendRpcCommandRequestComponent, che innesca il sistema di invio della RPC di Unity.

#### Sistema `GoInGameClientSystem`

L'attributo [UpdateInGroup(typeof(ClientSimulationSystemGroup))] indica che questo sistema dev'essere
aggiornato solo nei client, all'interno del gruppo ClientSimulationSystemGroup.<br/>
Vogliamo che questo sistema esegua una sola volta, quando il client deve entrare in gioco, per la precisione
dopo la connessione con il server, ma prima che venga avviata la comunicazione via comandi e snapshot.
Dunque, richiediamo che sia presente il singleton EnableGame e che l'entità rappresentante la connessione
(che possiede il componente <b>NetworkIdComponent</b>), non abbia <b>NetworkStreamInGame</b>.
```csharp
protected override void OnCreate()
{
    RequireSingletonForUpdate<EnableGame>();
    RequireForUpdate(GetEntityQuery(ComponentType.ReadOnly<NetworkIdComponent>(), ComponentType.Exclude<NetworkStreamInGame>()));
}
```

Dopodiché nella OnUpdate(), iteriamo su tutte le entità che possiedono <b>NetworkIdComponent</b> ma non hanno
<b>NetworkStreamInGame</b>, ovvero l'entità della connessione. Dunque, utilizzando un command buffer, seguiamo 
la procedura per inviare la RPC: creiamo un'entità, vi aggiungiamo il comando RPC, ed infine aggiungiamo il
componente <b>SendRpcCommandRequestComponent</b> indicando la connessione target.
```csharp
protected override void OnUpdate()
{
    var commandBuffer = new EntityCommandBuffer(Allocator.Temp);
    Entities.WithNone<NetworkStreamInGame>().ForEach((Entity ent, in NetworkIdComponent id) =>
    {
        commandBuffer.AddComponent<NetworkStreamInGame>(ent);
        var req = commandBuffer.CreateEntity();
        commandBuffer.AddComponent<GoInGameRequest>(req);
        commandBuffer.AddComponent(req, new SendRpcCommandRequestComponent { TargetConnection = ent });
    }).Run();
    commandBuffer.Playback(EntityManager);
    commandBuffer.Dispose();
}
```

#### Sistema `GoInGameServerSystem`

L'attributo [UpdateInGroup(typeof(ServerSimulationSystemGroup))] indica che questo sistema dev'essere
aggiornato solo nel server.<br/>
Vogliamo che questo sistema esegua solo quando, dopo che è stato aggiunto il singleton EnableGame, arriva 
una richiesta di RPC da un client. Dunque, richiediamo che sia presente EnableGame e che vi sia un'entità
avente come componenti il nostro comando RPC e <b>ReceiveRpcCommandRequestComponent</b>.
```csharp
protected override void OnCreate()
{
    RequireSingletonForUpdate<EnableGame>();
    RequireForUpdate(GetEntityQuery(ComponentType.ReadOnly<GoInGameRequest>(), ComponentType.ReadOnly<ReceiveRpcCommandRequestComponent>()));
}
```

Nella OnUpdate() otteniamo la lista dei ghost prefab, ovvero i networked object. Nel nostro prototipo
l'unico ghost presente è la PlayerCapsule, ovvero il personaggio che ciascun giocatore controlla e muove per
la mappa. Poiché in futuro questa lista potrebbe essere ampliata, controlliamo comunque che il ghost sia
quello della capsula, ovvero se possiede il componente PlayerMovementSpeed, e lo salviamo in una
variabile.<br/>
Dopodiché otteniamo la lista dei <b>NetworkIdComponent</b> delle connessioni, salvandola in networkIdFromEntity,
ovvero un container <i>dictionary-like</i>. Tramite questo container possiamo assegnare il rispettivo id della 
connessione al componente <b>GhostOwnerComponent</b> del ghost di ciascun client. Questa è un'operazione 
fondamentale che bisogna fare "a runtime", in quanto prima non è possibile conoscere a chi apparterrà un certo
ghost.
<br/>
Dunque iteriamo su tutte le entità che corrispondono a richieste RPC (aventi dunque GoInGameRequest e
ReceiveRpcCommandRequestComponent). Poiché nella richiesta è presente l'entità della connessione sorgente
da cui è partita la RPC, possiamo utilizzarla per aggiungervi il componente <b>NetworkStreamInGame</b> e 
iniziare la comunicazione via comandi e snapshot.
<br/>
Fatto questo, istanziamo la capsula del giocatore e aggiorniamo il NetworkId del proprietario di tale ghost.
<br/>
Infine, aggiungiamo alla capsula il buffer su cui verranno accumulati gli input del giocatore, ed alla
connessione il componente <b>CommandTargetComponent</b> che servirà al sistema di gestione degli input
per capire a quale ghost applicare gli input ricevuti dal giocatore. Inoltre, distruggiamo l'entità della
richiesta RPC altrimenti il sistema continua ad eseguire all'infinito.
<br/>
Ora è tutto impostato correttamente per permettere al client di accumulare input ed inviarli al server 
sottoforma di comandi, ed al server di ricevere questi comandi, applicarli nella propria simulazione ed
inviare le snapshot (ovvero gli aggiornamenti dello stato di gioco) al client.
```csharp
protected override void OnUpdate()
{
    var ghostCollection = GetSingletonEntity<GhostPrefabCollectionComponent>();
    var prefab = Entity.Null;
    var prefabs = EntityManager.GetBuffer<GhostPrefabBuffer>(ghostCollection);
    for (int ghostId = 0; ghostId < prefabs.Length; ++ghostId)
    {
        if (EntityManager.HasComponent<PlayerMovementSpeed>(prefabs[ghostId].Value))
            prefab = prefabs[ghostId].Value;
    }

    var commandBuffer = new EntityCommandBuffer(Allocator.Temp);
    var networkIdFromEntity = GetComponentDataFromEntity<NetworkIdComponent>(true);
    Entities.WithReadOnly(networkIdFromEntity).ForEach((Entity reqEnt, in GoInGameRequest req, in ReceiveRpcCommandRequestComponent reqSrc) =>
    {
        commandBuffer.AddComponent<NetworkStreamInGame>(reqSrc.SourceConnection);
        UnityEngine.Debug.Log(String.Format("Server setting connection {0} to in game", networkIdFromEntity[reqSrc.SourceConnection].Value));

        var player = commandBuffer.Instantiate(prefab); // spawn capsula per il giocatore
        commandBuffer.SetComponent(player, new GhostOwnerComponent { NetworkId = networkIdFromEntity[reqSrc.SourceConnection].Value });

        commandBuffer.AddBuffer<PlayerInput>(player);
        commandBuffer.SetComponent(reqSrc.SourceConnection, new CommandTargetComponent { targetEntity = player });

        commandBuffer.DestroyEntity(reqEnt);
    }).Run();
    commandBuffer.Playback(EntityManager);
    commandBuffer.Dispose();
}
```
</details>


### Input
<details>
Il file <a href="/DOTS%20Prototype/Assets/Scripts/Systems/PlayerMovementSystem.cs">PlayerInputSystem.cs</a> contiene la logica per l'accumulo degli input del giocatore. Essendo questo un gioco multiplayer, non basta semplicemente campionare l'input e usarlo direttamente, ma è necessario immagazzinarlo da qualche parte (una struttura <b><a href="https://docs.unity3d.com/Packages/com.unity.netcode@0.6/api/Unity.NetCode.ICommandData.html?q=ICommandData">ICommandData</a></b>) ed inviarlo al Server sotto forma di comando, così che anche lui possa applicarlo nella propria simulazione. Infatti, poiché NetCode si basa su un modello a server autoritativo, la simulazione viene eseguita sia su client che su server, ma il server ha l'autorità, ovvero la sua simulazione è sempre corretta ed il client deve correggere la propria in base a questa.

#### Comando `PlayerInput`
La struttura PlayerInput implementa l'interfaccia ICommandData, ovvero l'interfaccia necessaria per realizzare un comando in NetCode. Questa non è altro che un <a href="https://docs.unity3d.com/Packages/com.unity.entities@0.17/manual/dynamic_buffers.html#:~:text=A%20DynamicBuffer%20is%20a%20type,the%20internal%20capacity%20is%20exhausted.">buffer dinamico</a> utilizzato per accumulare comandi da trasmettere attraverso una connessione. Infatti, questa interfaccia espone la proprietà Tick, che dev'essere specificata, in quanto indica il tick di esecuzione della simulazione in cui è stato campionato l'input, così che il server, quando lo riceverà, potrà applicarlo nello stesso momento del client, indipendentemente dalla latenza della rete. Il tick permette anche di sfruttare la <a href="https://docs.unity3d.com/Packages/com.unity.netcode@0.6/manual/prediction.html">predizione lato client</a> fornita da NetCode.<br/>
Nel nostro caso questa struttura contiene, oltre al tick, i campi horizontal e vertical, che indicano rispettivamente il movimento sull'asse x e sull'asse y.
```csharp
public struct PlayerInput : ICommandData
{
	public uint Tick { get; set; }
	public int horizontal;
	public int vertical;
}
```

#### Sistema `PlayerInputSystem`
La raccolta degli input avviene tramite il sistema <b>PlayerInputSystem</b>, che esegue solo lato client. All'interno di questo, in OnCreate(), innanzitutto richiediamo che, affinché il sistema venga aggiornato, siano presenti il singleton <b>NetworkIdComponent</b> (che identifica una connessione, dunque un client) ed EnableGame (che indica che il gioco è iniziato). Poi salviamo in una variabile il gruppo di sistema <b>ClientSimulationSystemGroup</b>, in quanto da questo possiamo ottenere il tick del server (che aggiorna sempre ad un timestep fisso).
```csharp
ClientSimulationSystemGroup m_ClientSimulationSystemGroup;
protected override void OnCreate()
{
	RequireSingletonForUpdate<NetworkIdComponent>();
	RequireSingletonForUpdate<EnableGame>();
	m_ClientSimulationSystemGroup = World.GetExistingSystem<ClientSimulationSystemGroup>();
}
```

La parte più complicata di questo sistema risiede nel metodo OnUpdate(): dopo aver ottenuto il singleton <b>CommandTargetComponent</b>, controlliamo che contenga il  riferimento all'entità capsula del giocatore. Poiché a runtime ci possono essere diversi giocatori, e di conseguenza diversi personaggi capsula, è necessario distinguere il client a cui appartengono. Il componente CommandTargetComponent serve proprio a questo: è un singleton, diverso per ogni client. Infatti, quando l'applicazione viene messa in esecuzione normalmente, è presente solo il World del client specifico, di conseguenza il singleton rappresenta l'entità ghost della capsula associata al client del mondo.
Però, poiché alla prima esecuzione questo componente non è inizializzato, dobbiamo gestire anche il caso in cui non contenga ancora l'entità. In questo caso semplicemente otteniamo l'id della connessione dal singleton NetworkIdComponent e, iterando su tutte le entità capsula, cerchiamo quella con il <b>NetworkId</b> (nel componente <b>GhostOwner</b>, che avevamo inizializzato in Game.cs) corrispondente. Una volta trovata, impostiamo il valore di targetEntity di CommandTargetComponent.
```csharp
var localInput = GetSingleton<CommandTargetComponent>().targetEntity; 
if (localInput == Entity.Null)
{
	var localPlayerId = GetSingleton<NetworkIdComponent>().Value;
	var commandBuffer = new EntityCommandBuffer(Allocator.Temp);
	var commandTargetEntity = GetSingletonEntity<CommandTargetComponent>();
	Entities.WithAll<PlayerMovementSpeed>().WithNone<PlayerInput>()
	.ForEach((Entity ent, ref GhostOwnerComponent ghostOwner) =>
	{
	if (ghostOwner.NetworkId == localPlayerId)
	{
		commandBuffer.AddBuffer<PlayerInput>(ent);
		commandBuffer.SetComponent(commandTargetEntity, new CommandTargetComponent { targetEntity = ent });
	}
	}).Run();
	commandBuffer.Playback(EntityManager);
	return;
}
```

Fatto ciò possiamo finalmente campionare gli input: dopo aver aggiornato il tick del comando, con quello del server, ottenuto da ClientSimulationSystemGroup, impostiamo il valore di horizontal e vertical in base all'input ricevuto dall'utente. Infine, aggiungiamo l'input al buffer di comandi PlayerInput.
```csharp
var input = default(PlayerInput);
input.Tick = m_ClientSimulationSystemGroup.ServerTick;
if (Input.GetKey("a"))
	input.horizontal -= 1;
if (Input.GetKey("d"))
	input.horizontal += 1;
if (Input.GetKey("s"))
	input.vertical -= 1;
if (Input.GetKey("w"))
	input.vertical += 1;
var inputBuffer = EntityManager.GetBuffer<PlayerInput>(localInput);
inputBuffer.AddCommandData(input);
```
</details>


### Movimento
<details>
Il file <a href="/DOTS%20Prototype/Assets/Scripts/Systems/PlayerMovementSystem.cs">PlayerMovementSystem.cs</a> contiene la logica per l'applicazione del movimento alle capsule dei giocatori, sfruttando la predizione. 

#### Componente `PlayerMovementSpeed`
È associato a un'entità capsula e ne indica la velocità di movimento.

#### Sistema `PlayerMovementSystem`
Questo sistema viene aggiornato all'interno del gruppo <b>GhostPredictionSystemGroup</b>, che permette di implementare la predizione lato client dei ghost.
In particolare, nella OnUpdate() otteniamo il tick di predizione da tale gruppo e iteriamo su tutte le entità capsule, inserendo nella lambda i componenti che ci serviranno.
Come prima cosa controlliamo se il codice della predizione dovrebbe eseguire, utilizzando il metodo <b>ShouldPredict()</b> per sapere se all'entità dev'essere applicata la predizione per il tick in questione. In caso affermativo, dal buffer PlayerInput otteniamo il comando relativo a tale tick, e applichiamo il movimento in base ai dati contenuti nel comando.
```csharp
var tick = m_GhostPredictionSystemGroup.PredictingTick;
var deltaTime = Time.DeltaTime;
Entities.ForEach((DynamicBuffer<PlayerInput> inputBuffer, ref PhysicsVelocity pv, in PredictedGhostComponent prediction, in PlayerMovementSpeed pms) =>
{
	if (!GhostPredictionSystemGroup.ShouldPredict(tick, prediction))
		return;
	PlayerInput input;
	inputBuffer.GetDataAtTick(tick, out input);
	var speed = pms.speed;
	
	if (input.horizontal > 0)
		pv.Linear.x += speed * deltaTime;
	if (input.horizontal < 0)
		pv.Linear.x -= speed * deltaTime;
	if (input.vertical > 0)
		pv.Linear.z += speed * deltaTime;
	if (input.vertical < 0)
		pv.Linear.z -= speed * deltaTime;
}).ScheduleParallel();
```
</details>


### Visuale in Terza Persona
<details>
Il file <a href="/DOTS%20Prototype/Assets/Scripts/Systems/CameraFollowSystem.cs">CameraFollowSystem.cs</a> permette di realizzare una visuale di gioco in terza persona, in cui la camera principale segue il proprio personaggio capsula.

#### Sistema `CameraFollowSystem`
Come per PlayerInputSystem, questo sistema esegue nel gruppo ClientSimulationSystemGroup, in quanto la logica che realizza mostra un risultato diverso a seconda del client che esegue.
Il metodo OnUpdate() semplicemente salva in una variabile la posizione della camera principale <b>Camera.main</b> e, dopo aver ottenuto il singleton CommandTargetComponent contenente l'entità della capsula corrispondente al client, si cicla su tutte le entità capsule attualmente presenti a tempo di esecuzione. Dunque, si cerca l'entità corrispondente a quella contenuta in CommandTargetComponent, e si aggiorna la posizione della camera con quella della capsula, aggiungendovi un offset per avere una visuale completa. L'offset è ottenuto da un componente <b>PlayerCameraFollowComponent</b>, allegato all'entità capsula.
```csharp
var position = Camera.main.transform.position;

var commandTargetComponentEntity = GetSingletonEntity<CommandTargetComponent>();
var commandTargetComponent = GetComponent<CommandTargetComponent>(commandTargetComponentEntity);
Entities.WithAll<PlayerScoreComponent>().ForEach((Entity entity, in Translation translation, in PlayerCameraFollowComponent pcf) =>
{
	if (entity == commandTargetComponent.targetEntity && !pcf.fixedCamera)
	{
		position.x = translation.Value.x + pcf.xOffset;
		position.y = translation.Value.y + pcf.yOffset;
		position.z = translation.Value.z + pcf.zOffset;
	}
}).Run();
Camera.main.transform.position = position;
```
</details>


### Portali Cambia-Colore 
<details>
I file <a href="/DOTS%20Prototype/Assets/Scripts/Systems/TemporaryChangeMaterialOnTriggerSystem.cs">TemporaryChangeMaterialOnTriggerSystem.cs</a> e <a href="/DOTS%20Prototype/Assets/Scripts/Systems/PersistentChangeMaterialOnTriggerSystem.cs">PersistentChangeMaterialOnTriggerSystem.cs</a> contengono la logica per cambiare il materiale del personaggio capsula che li attraversa. In particolare, questi sistemi rilevano gli eventi trigger causati dal passaggio di un personaggio capsula attraverso un portale avente rispettivamente il componente <b>TemporaryChangeMaterialOnTriggerComponent</b> e <b>PersistentChangeMaterialOnTriggerTagComponent</b>. Quindi modificano il materiale (dunque anche il colore) della capsula in modo temporaneo, finché la capsula non esce dal portale, oppure persistente.

#### Sistema `TemporaryChangeMaterialOnTriggerSystem`
Questo sistema itera sulle entità aventi un buffer di componenti <b>StatefulTriggerEvent</b> ed il componente <b>TemporaryChangeMaterialOnTriggerComponent</b>:
* <b>StatefulTriggerEvent</b> è contenuto nel file <a href="/DOTS%20Prototype/Assets/Scripts/Components/DynamicBufferTriggerEventAuthoring.cs">DynamicBufferTriggerEventAuthoring.cs</a> e permette di accumulare eventi di tipo Trigger (lanciati quando una oggetto attraversa un portale, tramite le proprietà del componente PhysicsShape di quest'ultimo). Tramite questo possiamo sapere il frame esatto di entrata ed uscita dal portale, oltre che i frame in cui un'entità rimane all'interno di esso, poiché vengono bufferizzati gli eventi Trigger singoli e si controlla lo stato del frame precedente. Tale file è stato preso dalla sub-repository <a href="https://github.com/Unity-Technologies/EntityComponentSystemSamples/blob/master/UnityPhysicsSamples/Documentation/samples.md">UnityPhysicsSamples</a> di Unity, in cui vi sono diversi esempi per l'utilizzo del package Physics.
* <b>TemporaryChangeMaterialOnTriggerComponent</b> contiene l'entità di cui il portale cambierà il materiale, ogni volta che questa entrerà nel portale.

All'interno del ForEach, iteriamo sugli eventi trigger del buffer, che contengono l'entità con la quale il portale ha avuto la collisione, controllando in particolare quando questa entra o esce:
* Quando entra, si aggiorna il materiale dell'entità con quello del portale.
* Quando esce, si ripristina il materiale originale dell'entità.
In questo modo, viene resettato il materiale originale dell'entità, non quello precedente all'ingresso nel portale.
```csharp
Entities.WithoutBurst().ForEach((Entity e, ref DynamicBuffer<StatefulTriggerEvent> triggerEventBuffer, ref TemporaryChangeMaterialOnTriggerComponent changeMaterial) =>
{
	for (int i = 0; i < triggerEventBuffer.Length; i++)
	{
		var triggerEvent = triggerEventBuffer[i];
		var otherEntity = triggerEvent.GetOtherEntity(e);
		
		// exclude other triggers and processed events
		if (triggerEvent.State == EventOverlapState.Stay || !nonTriggerMask.Matches(otherEntity))
		{
			continue;
		}
		if (triggerEvent.State == EventOverlapState.Enter)
		{
			var volumeRenderMesh = EntityManager.GetSharedComponentData<RenderMesh>(e);
			var overlappingRenderMesh = EntityManager.GetSharedComponentData<RenderMesh>(otherEntity);
			overlappingRenderMesh.material = volumeRenderMesh.material;
			commandBuffer.SetSharedComponent(otherEntity, overlappingRenderMesh);
		}
		else
		{
			// State == PhysicsEventState.Exit
			if (changeMaterial.ReferenceEntity == Entity.Null)
			{
				continue;
			}
			var overlappingRenderMesh = EntityManager.GetSharedComponentData<RenderMesh>(otherEntity);
			var referenceRenderMesh = EntityManager.GetSharedComponentData<RenderMesh>(changeMaterial.ReferenceEntity);
			overlappingRenderMesh.material = referenceRenderMesh.material;
			commandBuffer.SetSharedComponent(otherEntity, overlappingRenderMesh);
		}
	}
}).Run();
```

#### Sistema `PersistentChangeMaterialOnTriggerSystem`
Il sistema PersistentChangeMaterialOnTriggerSystem è una versione semplificata di quello temporaneo. A differenza del precedente, non si gestisce la casistica in cui l'entità che attraversa il portale esca. Per questo motivo si utilizza il componente <b>PersistentChangeMaterialOnTriggerTagComponent</b> che non contiene alcun tipo di informazione, ma serve solo per indicare che un'entità è un portale.
</details>


### Teletrasporto
<details>
I file <a href="/DOTS%20Prototype/Assets/Scripts/Components/TeleportComponent.cs">TeleportComponent.cs</a> e <a href="/DOTS%20Prototype/Assets/Scripts/Systems/TeleportSystem.cs">TeleportSystem.cs</a> contengono rispettivamente lo stato e la logica per realizzare il teletrasporto di una capsula fra due portali "compagni".

#### Componente `TeleportComponent`
Questo componente indica che l'entità a cui è attaccato è un portale per il teletrasporto e contiene due proprietà:
* L'entità del portale compagno, che serve per identificare da dove usciranno le entità che attraversano il portale a cui è allegato il componente.
* Il numero di teletrasporti, che serve invece per evitare che l'entità che attraversa il portale non venga immediatamente riportata indietro.
```csharp
[GenerateAuthoringComponent]
public struct TeleportComponent : IComponentData
{
	public Entity Companion;
	public int TransferCount;
}
```

#### Sistema `TeleportSystem`
Questo sistema, nel metodo OnCreate() inizializza il contatore dei trasferimenti a 0.
```csharp
Entities.ForEach((ref TeleportComponent tc) =>
{
	tc.TransferCount = 0;
}).Run();
```

Nel metodo OnUpdate() iteriamo su tutte le entità aventi il componente <b>TeleportComponent</b> ed un buffer di <b>StatefulTriggerEvent</b>. Dentro al ForEach, salviamo in una variabile l'entità del portale compagno, quindi iteriamo su tutti gli eventi trigger contenuti nel buffer.
All'interno del ciclo for salviamo l'entità che ha innescato il trigger con il portale in una variabile (otherEntity), dopodiché controlliamo se questa è appena stata teletrasportata e, in questo caso, decrementiamo di 1 il valore di TransferCount.
Physics utilizza <b>RigidTransform</b> per indicare la posizione di un'entità nel "world-space" e applicarvi la simulazione fisica. Il portale (come nel nostro caso, in cui il teletrasporto effettivo è solo la superficie interna di un prefab) può essere parte di una gerarchia, dunque i componenti Translation e Rotation, che ne indicano la posizione, potrebbero non essere in coordinate globali (rispetto al world-space), ma relative all'entità padre nella gerarchia. Per questo motivo, salviamo in delle variabili le posizioni dei portali come RigidTransform, controllando se l'entità fa match con la maschera hierarchyChildMask (la quale contiene una query che controlla se ha i componenti Parent e LocalToWorld):
* in caso affermativo, significa che l'entità del portale è parte di una gerarchia, dunque utilizziamo il metodo DecomposeRigidBodyTransform() per ottenere un RigidTransform che ne indica la posizione nel "world-space", così che Physics possa utilizzarlo correttamente;
* in caso negativo, utilizziamo semplicemente la posizione corrente del portale (Translation e Rotation) per creare RigidTransform.
```csharp
var portalTransform = hierarchyChildMask.Matches(portalEntity)
? Math.DecomposeRigidBodyTransform(GetComponent<LocalToWorld>(portalEntity).Value)
: new RigidTransform(GetComponent<Rotation>(portalEntity).Value, GetComponent<Translation>(portalEntity).Value);
var companionTransform = hierarchyChildMask.Matches(companionEntity)
? Math.DecomposeRigidBodyTransform(GetComponent<LocalToWorld>(companionEntity).Value)
: new RigidTransform(GetComponent<Rotation>(companionEntity).Value, GetComponent<Translation>(companionEntity).Value);
```

Dopodiché calcoliamo l'offset di posizione e rotazione fra i portali, otteniamo i componenti relativi a posizione, rotazione e velocità dell'entità che l'ha attraversato, e vi applichiamo rispettivamente:
* una traslazione, per realizzare il teletrasporto;
* una rotazione, per aggiornare la direzione verso cui è rivolta;
* una rotazione, per aggiornare la direzione della velocità lineare.
Infine aggiorniamo il valore di questi e incrementiamo TransferCount di 1.
```csharp
var portalPositionOffset = companionTransform.pos - portalTransform.pos;
var portalRotationOffset = math.mul(companionTransform.rot, math.inverse(portalTransform.rot));

var entityPositionComponent = GetComponent<Translation>(otherEntity);
var entityRotationComponent = GetComponent<Rotation>(otherEntity);
var entityVelocityComponent = GetComponent<PhysicsVelocity>(otherEntity);

entityVelocityComponent.Linear = math.rotate(portalRotationOffset, entityVelocityComponent.Linear);
entityPositionComponent.Value += portalPositionOffset;
entityRotationComponent.Value = math.mul(entityRotationComponent.Value, portalRotationOffset);

SetComponent(otherEntity, entityPositionComponent);
SetComponent(otherEntity, entityRotationComponent);
SetComponent(otherEntity, entityVelocityComponent);

companionTeleportComponent.TransferCount++;
```

Per maggiori informazioni su come funziona il sistema che gestisce la posizione delle entità, fare riferimento a
<a href="https://docs.unity3d.com/Packages/com.unity.entities@0.17/manual/transform_system.html">TransformSystem</a>, mentre per quanto riguarda i calcoli matematici fatti per le gerarchie di entità <a href="https://docs.unity3d.com/Packages/com.unity.physics@0.6/api/Unity.Physics.Math.html">Physics.Math</a>.
</details>


### Spawn di Entità
<details>
Il file <a href="/DOTS%20Prototype/Assets/Scripts/Components/SpawnRandomObjectsAuthoring.cs">SpawnRandomObjectsAuthoring.cs</a> contiene la logica per lo spawn di un numero arbitrario di entità (dato un prefab) all'interno di un volume, in punti randomici. A differenza dei meccanismi precedenti, che sono divisi in file per i componenti e per i sistemi, questo è condensato tutto in un unico file. Il file è stato preso dalla sub-repository </a href="https://github.com/Unity-Technologies/EntityComponentSystemSamples/blob/master/UnityPhysicsSamples/Assets/Common/Scripts/SpawnRandomObjectsAuthoring.cs">Unity Physics Samples</a>

#### Componente `SpawnRandomObjectsAuthoring`
In questo caso, invece di utilizzare l'attributo [GenerateAuthoringComponent] abbiamo utilizzato il <a href="https://docs.unity3d.com/Packages/com.unity.entities@0.17/manual/conversion.html#the-iconvertgameobjecttoentity-interface">conversion workflow</a> di ECS, che ci permette di convertire un MonoBehaviour nel rispettivo componente.
Utilizzando l'interfaccia <b>IConvertGameObjectToEntity</b> ed il relativo metodo Convert convertiamo il MonoBehaviour in un componente <b>SpawnSettings</b>, creando e inizializzando la rispettiva struttura, aggiungendolo all'entità convertita dal GameObject.
```csharp
public void Convert(Entity entity, EntityManager dstManager, GameObjectConversionSystem conversionSystem)
{
	var spawnSettings = new T
	{
		Prefab = conversionSystem.GetPrimaryEntity(prefab),
		Position = transform.position,
		Rotation = transform.rotation,
		Range = range,
		Count = count
	};
	Configure(ref spawnSettings);
	dstManager.AddComponentData(entity, spawnSettings);
}
```

#### Sistema `SpawnRandomObjectsSystemBase`
Questo sistema si occupa dello spawn delle entità: all'interno del metodo OnUpdate(), utilizziamo un ciclo ForEach "rustico" (in quanto il sistema è di tipo generico T) per iterare sulle entità che hanno il componente SpawnSettings. All'interno di questo ciclo creiamo un NativeArray della dimensione di count, ovvero il numero di entità da spawnare, per contenere le istanze delle entità, e altri due NativeArray per le posizioni e le rotazioni.
Dunque utilizziamo il metodo <b>RandomPointsInRange()</b> per inizializzare questi ultimi due NativeArray ed iteriamo per il numero di entità da spawnare e per ciascuna impostiamo il componente Traslation e Rotation, così che possa comparire all'interno del mondo. Infine rimuoviamo il componente SpawnSettings dall'entità spawner, per impedire che il metodo OnUpdate() esegua di nuovo.
```csharp
var instances = new NativeArray<Entity>(count, Allocator.Temp);
EntityManager.Instantiate(spawnSettings.Prefab, instances);

var positions = new NativeArray<float3>(count, Allocator.Temp);
var rotations = new NativeArray<quaternion>(count, Allocator.Temp);
RandomPointsInRange(spawnSettings.Position, spawnSettings.Rotation, spawnSettings.Range, ref positions, ref rotations, GetRandomSeed(spawnSettings));

for (int i = 0; i < count; i++)
{
	var instance = instances[i];
	EntityManager.SetComponentData(instance, new Translation { Value = positions[i] });
	EntityManager.SetComponentData(instance, new Rotation { Value = rotations[i] });
	ConfigureInstance(instance, spawnSettings);
}
EntityManager.RemoveComponent<T>(entity);
```

Il metodo <b>RandomPointsInRange()</b> prende i valori del volume passati come parametri e genera un punto radomico all'interno di questo, aggiornando i valori di <b>Translation</b> e <b>Rotation</b> per ciascun elemento dei rispettivi array.
```csharp
protected static void RandomPointsInRange(
float3 center, quaternion orientation, float3 range,
ref NativeArray<float3> positions, ref NativeArray<quaternion> rotations, int seed = 0)
{
	var count = positions.Length;
	
	var random = new Unity.Mathematics.Random((uint)seed);
	for (int i = 0; i < count; i++)
	{
		positions[i] = center + math.mul(orientation, random.NextFloat3(-range, range));
		rotations[i] = math.mul(random.NextQuaternionRotation(), orientation);
	}
}
```
</details>


### Raccolta di Entità
<details>
Il file <a href="/DOTS%20Prototype/Assets/Scripts/Systems/PickUpSystem.cs">PickUpSystem.cs</a> contiene la logica per la raccolta delle entità "collectible". Quando un personaggio capsula tocca un'entità marcata con questo componente, l'entità viene raccolta, dunque scompare dalla scena e viene assegnato un punteggio al giocatore.

#### Componente `PlayerScoreComponent`
È assegnato al personaggio capsula di un giocatore e ne indica il punteggio corrente.

#### Componente `CollectibleTagComponent`
Indica che un'entità è raccoglibile e vi assegna un punteggio.

#### Componente `DeleteTagComponent`
È un componente vuoto che indica che un'entità dev'essere eliminata.

#### Sistema `PickUpSystem`
Questo sistema si occupa di rilevare gli eventi trigger tra un player capsula e un'entità collectible. Il funzionamento è simile a quello dei portali: all'interno del metodo OnUpdate() iteriamo su tutte le entità aventi il buffer di <b>StatefulTriggerEvent</b> e <b>CollectibleTagComponent</b>.
```csharp
Entities.WithoutBurst().ForEach(
(Entity e, ref DynamicBuffer<StatefulTriggerEvent> triggerEventBuffer, ref CollectibleTagComponent collectibleComponent) => {
```

Dopodiché eseguiamo un ciclo sugli eventi trigger contenuti nel buffer:
1. Otteniamo l'entità con cui è avvenuta la collisione.
2. Controlliamo che lo stato di StatefulTriggerEvent sia "Enter" e che l'entità con cui è avvenuta la collisione sia un personaggio capsula (ovvero abbia il componente <b>PlayerMovementSpeed</b>).
3. Otteniamo il componente <b>PlayerScoreComponent</b>, in cui si trova il punteggio attuale del giocatore e lo incrementiamo del valore contenuto in <b>CollectibleTagComponent</b>.
4. Aggiorniamo il valore di <b>PlayerScoreComponent</b> del giocatore e aggiungiamo il componente <b>DeleteTagComponent</b> all'entità collectible.
```csharp
var otherEntity = triggerEvent.GetOtherEntity(e); 

if (triggerEvent.State == EventOverlapState.Enter && EntityManager.HasComponent<PlayerMovementSpeed>(otherEntity))
{
	var punteggioPlayer = EntityManager.GetComponentData<PlayerScoreComponent>(otherEntity);
	punteggioPlayer.score += collectibleComponent.points;

	commandBuffer.SetComponent(otherEntity, punteggioPlayer);
	commandBuffer.AddComponent<DeleteTagComponent>(e, new DeleteTagComponent());
}
```

#### Sistema `DeleteCollectibleSystem`
Questo sistema si occupa dell'eliminazione delle entità marcate col componente <b>DeleteTagComponent</b>. Semplicemente itera su tutte le entità aventi tale componente e, utilizzando un command buffer, le elimina.
```csharp
Entities.WithAll<DeleteTagComponent>().ForEach((Entity entity) =>
{
	commandBuffer.DestroyEntity(entity);
}).Run();
```

Questa funzionalità poteva essere realizzata direttamente utilizzando solo CollectibleTagComponent e PickUpSystem, realizzando l'eliminazione dell'entità direttamente all'interno di quest'ultimo, ma abbiamo voluto separare le competenze mostrando un'ulteriore possibilità.
</details>


## Riferimenti Utili


### Documentazione
* <a href="https://docs.unity3d.com/Manual/index.html">Unity Manual</a>
* <a href="https://docs.unity3d.com/Packages/com.unity.entities@0.17">Unity Entities</a>
* <a href="https://docs.unity3d.com/Packages/com.unity.physics@0.6">Unity Physics</a>
* <a href="https://docs.unity3d.com/Packages/com.unity.netcode@0.6">Unity NetCode</a>
* <a href="https://youtube.com/playlist?list=PLX2vGYjWbI0S1wHRTyDiPtKLEPTWFi4cd">Unity Copenhagen 2019 - DOTS (YouTube Playlist)</a>
<!--<iframe width="560" height="315" src="https://www.youtube.com/embed/BNMrevfB6Q0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>-->

### Repository GitHub
* <a href="https://github.com/Unity-Technologies/DOTSSample">DOTS Sample</a> - uno sparatutto multigiocatore completo realizzato utilizzando DOTS.
* <a href="https://github.com/Unity-Technologies/EntityComponentSystemSamples">EntityComponentSystemSamples</a> - contiene delle sub-repository, fra cui anche UnityPhysicsSamples, con esempi, demo e use cases molto utili.
* <a href="https://github.com/Unity-Technologies/DOTS-training-samples">DOTS training samples</a> - contiene piccole simulazioni e giochi implementati utilizzando l'architettura classica (senza DOTS) di Unity. È una repository utile per allenarsi a usare DOTS.
* <a href="https://github.com/Unity-Technologies/multiplayer">Unity Real-time Multiplayer Alpha</a> - contiene un progetto d'esempio che utilizza NetCode per realizzare la parte di networking.
* <a href="https://github.com/Unity-Technologies/FPSSample">FPS Sample</a> - obsoleto ma è un progetto interessante.
* <a href="https://github.com/UnityTechnologies/AngryBots_ECS">AngryBots ECS</a> - semplice gioco in terza persona che mostra in modo semplice alcuni vantaggi dell'utilizzo di DOTS.

### Forum DOTS
Clicca <a href="https://forum.unity.com/forums/data-oriented-technology-stack.147/">qui</a> per visitare il forum.

---
title: C# Available Methods
description: 
published: true
date: 2022-07-21T20:25:22.040Z
tags: 
editor: markdown
dateCreated: 2021-08-25T21:31:38.226Z
---


Below are all the methods that can be accessed via the `CPH` object that is is available in your inline scripts

> *Some early info, CPH is a hold over from earlier versions of the application where it was known as Channel Points Handler, to prevent any breakage, and as a bit of nostalgia CPH was left when the rename happened to Streamer.bot*
{.is-info}

If there are methods missing, make the suggestion to get them added in!

# Application

## General

```csharp
int Between(int min, int max);
double NextDouble(); // get a random value between 0f and 1f
```

```csharp
void Wait(int milliseconds);
```

```csharp
string UrlEncode(string text);
string EscapeString(string text);
```

```csharp
EventSource GetSource();
EventType GetEventType();
```

## Logging

```csharp
void LogInfo(string logLine);
void LogWarn(string logLine);
void LogDebug(string logLine);
```

## Credits & First Words

```csharp
void AddToCredits(string section, string value, bool json = true)
```

```csharp
void ResetCredits();
void ResetFirstWords();
```

## Timers

```csharp
void DisableTimer(string timerName);
void EnableTimer(string timerName);
```

## Variables

```csharp
void SetArgument(string variableName, object value); // set an argument to be used in subsequent sub-actions
```

## Global Variables

```csharp
T GetGlobalVar<T>(string varName, bool persisted = true);
void SetGlobalVar(string varName, object value, bool persisted = true);
void UnsetGlobalVar(string varName, bool persisted = true);
T GetUserVar<T>(string userName, string varName, bool persisted = true);
void SetUserVar(string userName, string varName, object value, bool persisted = true);
void UnsetUserVar(string userName, string varName, bool persisted = true);
void UnsetUser(string userName, bool persisted = true);
```

## Groups

```csharp
bool UserInGroup(int userId, string groupName);
bool UserInGroup(string userName, string groupName);
bool AddUserToGroup(int userId, string groupName);
bool AddUserToGroup(string userName, string groupName);
bool RemoveUserFromGroup(int userId, string groupName);
bool RemoveUserFromGroup(string userName, string groupName);
```

## Commands

### Enable/Disable Commands
```csharp
void EnableCommand(string id);
void DisableCommand(string id);
```

### Set Commands Cooldowns
> Requires minimum version 0.1.8
{.is-info}
```csharp
void CommandSetGlobalCooldownDuration(string id, int seconds);
void CommandSetUserCooldownDuration(string id, int seconds);
```

### Add to Commands Cooldowns
```csharp
void CommandAddToGlobalCooldown(string id, int seconds);
void CommandAddToUserCooldown(string id, int userId, int seconds);
void CommandAddToAllUserCooldowns(string id, int seconds);
```

### Reset Commands Cooldowns
```csharp
void CommandResetGlobalCooldown(string id);
void CommandResetUserCooldown(string id, int userId);
void CommandResetAllUserCooldowns(string id);
```
# Servers and Clients

## Websocket Server

```csharp
void WebsocketBroadcastString(string data); // send a custom event over the websocket server
void WebsocketBroadcastJson(string data); // send a custom event over the websocket server
```

## Websocket Clients

```csharp
void WebsocketConnect(int connection = 0);
void WebsocketDisconnect(int connection = 0);
bool WebsocketIsConnected(int connection = 0);
void WebsocketSend(string data, int connection = 0);
void WebsocketSend(byte[] data, int connection = 0);
```

## Custom Websocket Servers

```csharp
void WebsocketCustomServerStart(int connection = 0);
void WebsocketCustomServerStop(int connection = 0);
bool WebsocketCustomServerIsListening(int connection = 0);
void WebsocketCustomServerCloseAllSessions(int connection = 0);
void WebsocketCustomServerCloseSession(string sessionId, int connection = 0);
void WebsocketCustomServerBroadcast(string data, string sessionId, int connection = 0);
```

> Requires minimum version 0.1.8
{.is-info}
```csharp
int WebsocketCustomServerGetConnectionByName(string name);
```

# Actions

## General

```csharp
bool RunAction(string actionName, bool runImmediately = true);
```

> Requires minimum version 0.1.8
{.is-info}
```csharp
bool RunActionById(string actionId, bool runImmediately = true);
```

```csharp
void DisableAction(string actionName);
void EnableAction(string actionName);
```

## Action Queues

```csharp
void PauseActionQueue(string name);
void PauseAllActionQueues();
void ResumeActionQueue(string name, bool clear = false);
void ResumeAllActionQueues(bool clear = false);
```

## UDP Broadcast

```csharp
int BroadcastUdp(int port, object data);
```

## Sound

```csharp
void PlaySound(string fileName, float volume = 1.0f, bool finishBeforeContinuing = false);
void PlaySoundFromFolder(string path, float volume = 1.0f, bool recursive = false, bool finishBeforeContinuing = false);
```

> The two methods were originally written on the wiki as finishBeforeContinuing = true, this was incorrect, the default is false for this parameter.
{.is-danger}

## TwitchSpeaker

```csharp
int TtsSpeak(string voiceAlias, string message, bool badWordFilter = false);
```

## Keyboard Press

```csharp
void KeyboardPress(string keyPress);
```

## C# Execute Method

```csharp
bool ExecuteMethod(string executeCode, string methodName);
```

# Twitch

## General

```csharp
void SendMessage(string message, bool bot = true);
void SendAction(string action, bool bot = true);
void SendWhisper(string userName, string message);
void TimeoutUser(string userName, int duration);
```
```csharp
List<Cheermote> GetCheermotes();
```

```csharp
void TwitchSubscriberOnly(bool enabled = true);
void TwitchEmoteOnly(bool enabled = true);
```

## Channel Rewards

```csharp
void DisableReward(string rewardId);
void EnableReward(string rewardId);
void PauseReward(string rewardId);
void UnPauseReward(string rewardId);
```

```csharp
void UpdateRewardCost(string rewardId, int cost, bool additive = false);
void UpdateRewardCooldown(string rewardId, int cooldown, bool additive = false);
```

```csharp
string TwitchRedemptionFulfill(string rewardId, string redemptionId);
string TwitchRedemptionCancel(string rewardId, string redemptionId);
```

> Requires minimum version 0.1.5
{.is-info}

> Return value changed to bool in version 0.1.9
{.is-info}

```csharp
bool UpdateRewardTitle(string rewardId, string title);
bool UpdateRewardPrompt(string rewardId, string prompt);
bool UpdateReward(string rewardId, string title = null, string prompt = null, int? cost = null);
```

## Polls

```csharp
bool TwitchPollCreate(string title, List<string> choices, int duration, int bitsPerVote = 0, int channelPointsPerVote = 0);
void TwitchPollTerminate(string pollId);
void TwitchPollArchive(string pollId);
```

## Predictions

```csharp
string TwitchPredictionCreate(string title, List<string> options, int duration);
void TwitchPredictionCancel(string predictionId);
void TwitchPredictionLock(string predictionId);
void TwitchPredictionResolve(string predictionId, string winningId);
```

## Clips

> All clip data is returned as oldest to newest, this is a limitation of the Twitch API.  To get most recent clips, one would have to get all the clips for the user, one got-ya for this, there is a hard limit of 1000 clips that can be returned
{.is-info}

```csharp
List<ClipData> GetAllClips();
List<ClipData> GetClipsForGame(int gameId);
List<ClipData> GetClipsForUser(int userId);
List<ClipData> GetClipsForUser(string username);
```

```csharp
ClipData CreateClip();
```

> Requires minimum version 0.1.5
{.is-info}

```csharp
List<ClipData> GetClipsForUser(int userId, int count);
List<ClipData> GetClipsForUser(int userId, DateTime start, DateTime end);
List<ClipData> GetClipsForUser(int userId, DateTime start, DateTime end, int count);
List<ClipData> GetClipsForUser(int userId, TimeSpan duration);
List<ClipData> GetClipsForUser(int userId, TimeSpan duration, int count);
List<ClipData> GetClipsForUser(string userName, int count);
List<ClipData> GetClipsForUser(string username, DateTime start, DateTime end);
List<ClipData> GetClipsForUser(string username, DateTime start, DateTime end, int count);
List<ClipData> GetClipsForUser(string username, TimeSpan duration);
List<ClipData> GetClipsForUser(string username, TimeSpan duration, int count);
List<ClipData> GetClipsForGame(int gameId, int count);
List<ClipData> GetClipsForGame(int gameId, DateTime start, DateTime end);
List<ClipData> GetClipsForGame(int gameId, DateTime start, DateTime end, int count);
List<ClipData> GetClipsForGame(int gameId, TimeSpan duration);
List<ClipData> GetClipsForGame(int gameId, TimeSpan duration, int count);
```

### ClipData contains the following values
```csharp
string Id;
string Url;
string EmbedUrl;
int BroadcasterId;
string BroadcasterName;
int CreatorId;
string CreatorName;
string VideoId;
string GameId;
string Language;
string Title;
int ViewCount;
DateTime CreatedAt;
string ThumbnailUrl;
float Duration;
```

## Markers

```csharp
StreamMarker CreateStreamMarker(string description);
```

### StreamMarker is the following class

```csharp
public class StreamMarker
{
	public int Id { get; set; }
    public DateTime CreatedAt { get; set; }
    public string Description { get; set; }
    public int Position { get; set; }
}
```

## Run Commercial

```csharp
void TwitchRunCommercial(int duration);
```

## Slow Mode

```csharp
void TwitchSlowMode(bool enabled = true, int duration = 0);
```

## Stream Update
```csharp
bool SetChannelTitle(string title);
GameInfo SetChannelGame(string game);
bool SetChannelGameById(string gameId);
```

## Announcement
> Requires minimum version 0.1.9
{.is-info}

> Even though the color parameter is present, currently, due to a Twitch limitation, only null is supported, this will use the default announce command.  When Twitch fixes this, supported values will be `blue`, `orange`, `green`, `purple`
{.is-warning}

```csharp
void TwitchAnnounce(string message, string color = null);
```

## OAuth & Client Id
> Requires minimum version 0.1.10
{.is-info}

```csharp
string TwitchOAuthToken();
```
```csharp
string TwitchClientId();
```

# YouTube
> Requires minimum version 0.1.8
{.is-info}

## Chat Message

```csharp
void SendYouTubeMessage(string message);
```

## User Variables

```csharp
T GetTwitchUserVar<T>(string userName, string varName, bool persisted = true);
T GetYouTubeUserVar<T>(string userName, string varName, bool persisted = true);
void SetTwitchUserVar(string userName, string varName, object value, bool persisted = true);
void SetYouTubeUserVar(string userName, string varName, object value, bool persisted = true);
void UnsetTwitchUserVar(string userName, string varName, bool persisted = true);
void UnsetYouTubeUserVar(string userName, string varName, bool persisted = true);
void UnsetTwitchUser(string userName, bool persisted = true);
void UnsetYouTubeUser(string userName, bool persisted = true);
```

# OBS

## Connection
```csharp
bool ObsIsConnected(int connection = 0);
bool ObsConnect(int connection = 0);
void ObsDisconnect(int connection = 0);
```

## Stream/Recording Status
```csharp
bool ObsIsStreaming(int connection = 0);
void ObsStopStreaming(int connection = 0);
bool ObsIsRecording(int connection = 0);
void ObsStartRecording(int connection = 0);
void ObsStopRecording(int connection = 0);
void ObsPauseRecording(int connection = 0);
void ObsResumeRecording(int connection = 0);
```

## Scenes
```csharp
void ObsSetScene(string sceneName, int connection = 0);
string ObsGetCurrentScene(int connection = 0);
```

## Sources
```csharp
bool ObsIsSourceVisible(string scene, string source, int connection = 0);
void ObsSetSourceVisibility(string scene, string source, bool visible, int connection = 0);
void ObsShowSource(string scene, string source, int connection = 0);
void ObsHideSource(string scene, string source, int connection = 0);
void ObsHideGroupsSources(string scene, string groupName, int connection = 0);
string ObsSetRandomGroupSourceVisible(string scene, string groupName, int connection = 0);
List<string> ObsGetGroupSources(string scene, string groupName, int connection = 0);
string ObsGetSceneItemProperties(string scene, string source, int connection = 0);
```

## Browser/Text Sources
```csharp
void ObsSetBrowserSource(string scene, string source, string url, int connection = 0);

// use '/n' for a new line e.g. line 1/nline 2
void ObsSetGdiText(string scene, string source, string text, int connection = 0);
```

## Filters
```csharp
bool ObsIsFilterEnabled(string scene, string filterName, int connection = 0);
bool ObsIsFilterEnabled(string scene, string source, string filterName, int connection = 0);
void ObsSetFilterState(string scene, string filterName, int state, int connection = 0);
void ObsSetFilterState(string scene, string source, string filterName, int state, int connection = 0);
void ObsShowFilter(string scene, string filterName, int connection = 0);
void ObsShowFilter(string scene, string source, string filterName, int connection = 0);
void ObsHideFilter(string scene, string filterName, int connection = 0);
void ObsHideFilter(string scene, string source, string filterName, int connection = 0);
void ObsToggleFilter(string scene, string filterName, int connection = 0);
void ObsToggleFilter(string scene, string source, string filterName, int connection = 0);
void ObsSetRandomFilterState(string scene, int state, int connection = 0);
void ObsSetRandomFilterState(string scene, string source, int state, int connection = 0);
```

## Mute
```csharp
void ObsSetSourceMuteState(string scene, string source, int state, int connection = 0);
void ObsSourceMute(string scene, string source, string filterName, int connection = 0);
void ObsSourceUnMute(string scene, string source, string filterName, int connection = 0);
void ObsSourceMuteToggle(string scene, string source, string filterName, int connection = 0);
```

## [Raw](/en/Sub-Actions/OBS/Raw)
> There was an error with the ObsSendRaw method, it does actually return the JSON string from the call for you to parse, and takes a JSON string for the data to send.  A changelog had this information, but forgot to update the list of methods.
{.is-info}

```csharp
string ObsSendRaw(string requestType, string data, int connection = 0);
```

## Hide All Scene/Source Filters
```csharp
void ObsHideSourcesFilters(string scene, string source, int connection = 0);
void ObsHideScenesFilters(string scene, int connection = 0);
```

## Media
```csharp
void ObsSetMediaState(string scene, string source, int state, int connection = 0);
void ObsMediaPlay(string scene, string source, int connection = 0);
void ObsMediaPause(string scene, string source, int connection = 0);
void ObsMediaRestart(string scene, string source, int connection = 0);
void ObsMediaStop(string scene, string source, int connection = 0);
void ObsMediaNext(string scene, string source, int connection = 0);
void ObsMediaPrevious(string scene, string source, int connection = 0);
```

## Colors
> Requires minimum version 0.1.5
{.is-info}

```csharp
long ObsConvertRgb(int a, int r, int g, int b);
long ObsConvertColorHex(string colorHex);
```

## Get Connection By Name
```csharp
int ObsGetConnectionByName(string name);
```

## Replay Buffer
```csharp
void ObsSetReplayBufferState(int state, int connection = 0);
void ObsReplayBufferStart(int connection = 0);
void ObsReplayBufferStop(int connection = 0);
void ObsReplayBufferSave(int connection = 0);
```

## Set Media Source File
```csharp
void ObsSetMediaSourceFile(string scene, string source, string file, int connection = 0);
```

## Set Image Source File
```csharp
void ObsSetImageSourceFile(string scene, string source, string file, int connection = 0);
```

# StreamLabs OBS

## Connection
```csharp
bool SlobsIsConnected(int connection = 0);
bool SlobsConnect(int connection = 0);
void SlobsDisconnect(int connection = 0);
```

## Stream/Recording Status
```csharp
bool SlobsIsStreaming(int connection = 0);
void SlobsStopStreaming(int connection = 0);
void SlobsStartStreaming(int connection = 0);
bool SlobsIsRecording(int connection = 0);
void SlobsStartRecording(int connection = 0);
void SlobsStopRecording(int connection = 0);
void SlobsPauseRecording(int connection = 0);
void SlobsResumeRecording(int connection = 0);
```

## Scenes
```csharp
void SlobsSetScene(string sceneName, int connection = 0);
string SlobsGetCurrentScene(int connection = 0);
```
## Sources
```csharp
bool SlobsIsSourceVisible(string scene, string source, int connection = 0);
void SlobsSetSourceVisibility(string scene, string source, bool visible, int connection = 0);
void SlobsShowSource(string scene, string source, int connection = 0);
void SlobsHideSource(string scene, string source, int connection = 0);
void SlobsHideGroupsSources(string scene, string groupName, int connection = 0);
string SlobsSetRandomGroupSourceVisible(string scene, string groupName, int connection = 0);
List<string> SlobsGetGroupSources(string scene, string groupName, int connection = 0);
```

## Browser/Text Sources
```csharp
void SlobsSetBrowserSource(string scene, string source, string url, int connection = 0);
void SlobsSetGdiText(string scene, string source, string text, int connection = 0);
```

## Filters
```csharp
bool SlobsIsFilterEnabled(string scene, string filterName, int connection = 0);
bool SlobsIsFilterEnabled(string scene, string source, string filterName, int connection = 0);
void SlobsSetFilterState(string scene, string filterName, int state, int connection = 0);
void SlobsSetFilterState(string scene, string source, string filterName, int state, int connection = 0);
void SlobsShowFilter(string scene, string filterName, int connection = 0);
void SlobsShowFilter(string scene, string source, string filterName, int connection = 0);
void SlobsHideFilter(string scene, string filterName, int connection = 0);
void SlobsHideFilter(string scene, string source, string filterName, int connection = 0);
void SlobsToggleFilter(string scene, string filterName, int connection = 0);
void SlobsToggleFilter(string scene, string source, string filterName, int connection = 0);
void SlobsSetRandomFilterState(string scene, int state, int connection = 0);
void SlobsSetRandomFilterState(string scene, string source, int state, int connection = 0);
```

## Mute
```csharp
void SlobsSetSourceMuteState(string scene, string source, int state, int connection = 0);
void SlobsSourceMute(string scene, string source, string filterName, int connection = 0);
void SlobsSourceUnMute(string scene, string source, string filterName, int connection = 0);
void SlobsSourceMuteToggle(string scene, string source, string filterName, int connection = 0);
```

# Voicemod
> Requires minimum version 0.1.8
{.is-info}

## Select Voice
```csharp
void VoiceModSelectVoice(string voiceId);
```

## Voice Changer On/Off
```csharp
bool VoiceModVoiceChangerOn();
bool VoiceModVoiceChangerOff();
```

## Hear My Voice On/Off
```csharp
bool VoiceModHearMyVoiceOn();
bool VoiceModHearMyVoiceOff();
```

## Censor On/Off
```csharp
void VoiceModCensorOn();
void VoiceModCensorOff();
```

## Get Current Voice
```csharp
string VoiceModGetCurrentVoice();
```

## Get Voice Changer Status
```csharp
bool VoiceModGetVoiceChangerStatus();
```

## Get Hear Myself Status
```csharp
bool VoiceModGetHearMyselfStatus();
```
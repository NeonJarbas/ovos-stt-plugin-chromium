## Description

A stt plugin for mycroft using the google chrome browser api

List of supported languages can be found [in this stackoverflow comment](https://stackoverflow.com/questions/14257598/what-are-language-codes-in-chromes-implementation-of-the-html5-speech-recogniti/14302134#14302134)

This STT API [has been deprecated](http://www.chromium.org/developers/how-tos/api-keys) for developers and no new keys are issued, however it still works, most likely due to it being [used in chromium](https://stackoverflow.com/questions/26485531/google-speech-api-v2), [a key is bundled](https://github.com/JarbasLingua/jarbas-stt-plugin-chromium/blob/61ab7c6917bf4fb0ebbdd1066109ac33a4da7704/jarbas_stt_plugin_chromium/__init__.py#L14) with this plugin that has been functional for a long time

This is the same as the "google" module in mycroft-core, while this engine is supported by mycroft-core, it is impossible to use because you can't get keys, this usage (of demo key) is disapproved and a [PR to fix this](https://github.com/MycroftAI/mycroft-core/pull/1493) has been blocked

By using this plugin you will lose some privacy (mycroft backend proxy) but will have less latency and more configuration options, while keeping the same accuracy, this is the same STT engine used by [Mycroft Selene](https://github.com/MycroftAI/selene-backend/blob/6f2de64f3bce70da2d82bdf5534338f5e7d3f9c3/api/public/public_api/endpoints/google_stt.py#L92)

## Install

`pip install ovos-stt-plugin-chromium`


## Configuration

By default the global language used by mycroft-core will be used

```json
  "stt": {
    "module": "ovos-stt-plugin-chromium"
  }
 
```

### Advanced configuration


```json
  "stt": {
    "module": "ovos-stt-plugin-chromium",
    "ovos-stt-plugin-chromium": {
        "lang": "en-US",
        "pfilter": false,
        "debug": false
    }
  }
 
```

`pfilter` - profanity filter, if True censors "bad words", only shows the first character and replaces the rest with asterisks. eg `f*** you`

`lang` - override core language and use this one instead

`debug` - log confidence and alternative transcriptions


## Docker

The privacy benefit is dubious at best, but this plugin can be used together with [ovos-stt-http-server](https://github.com/OpenVoiceOS/ovos-stt-http-server) to provide the equivalent of selene STT proxy functionality without pairing

```bash
docker run -p 8080:8080 ghcr.io/openvoiceos/google-stt-proxy:master
```

Public instances of [ovos-stt-http-server](https://github.com/OpenVoiceOS/ovos-stt-http-server) running this plugin:

- https://stt.openvoiceos.com hosted by [@OpenVoiceOS](https://github.com/OpenVoiceOS)
- https://stt.jarbasai.online hosted by [@JarbasAI](https://github.com/JarbasAl)
- https://stt.strongthany.cc hosted by [@Strongthany](https://twitter.com/strongthany_)

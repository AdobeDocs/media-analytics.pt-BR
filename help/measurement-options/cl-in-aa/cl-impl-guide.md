---
title: Guia de implementação do Link personalizado
description: null
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Guia de implementação de Link personalizado {#custom-link-implementation-guide}

O Rastreamento de vídeo personalizado usa o [rastreamento de link manual com o código de link personalizado](https://marketing.adobe.com/resources/help/pt_BR/sc/implement/link_manual.html) no Analytics `appMeasurement`. Na maioria das vezes, o rastreamento de vídeo com link personalizado é usado em plataformas e dispositivos que exigem o mínimo de medição de vídeo.

* No JavaScript: a função `s.tl()`
* Nos aplicativos móveis: [trackAction() Android](https://marketing.adobe.com/resources/help/pt_BR/mobile/android/actions.html), [trackAction() iOS](https://marketing.adobe.com/resources/help/pt_BR/mobile/ios/actions.html), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* Na API de inserção de dados: [linktype tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Requisitos

* Acesso a evento e dados da API do reprodutor de vídeo
* Capacidade de adicionar scripts se estiver usando o SDK do Analytics
* Capacidade de adicionar beacons de rastreamento (scripting ou hardcode personalizado) se estiver usando a API de inserção de dados

## Metadados

* Os metadados podem ser adicionados a qualquer chamada de rastreamento como parte dos dados de link
* Lembre-se de atualizar `linkTrackVars` e `linkTrackEvents`

```javascript
/* Call on video complete */ 
 
if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15'; 
    s.linkTrackEvents = 'event3'; 
    s.prop10 = mediaName; 
    s.eVar10 = mediaName; 
    s.eVar12 = "video"; 
    s.eVar13 = document.title; 
    s.eVar15 = mediaPlayerName; 
    s.events = 'event3'; 
    s.tl(this,'o','Video Complete'); 
};
```

## Por que usar um link personalizado

* Pré-requisitos mínimos são necessários
* Funciona em qualquer plataforma, incluindo sem script
* Qualquer cálculo, como tempo gasto ou quartis, deve ser calculado em um script personalizado
* Bastante simples, sem bibliotecas ou scripts ocultos
* Controle total sobre todos os aspectos dos dados de vídeo

## Exemplo de JavaScript para reprodutor HTML5

```javascript
<script type="text/javascript"> 
  myvideo = document.getElementById('movie'); 
  myvideo.addEventListener('play',myHandler,false); 
  myvideo.addEventListener('seeked',myHandler,false); 
  myvideo.addEventListener('seeking',myHandler,false); 
  myvideo.addEventListener('pause',myHandler,false); 
  myvideo.addEventListener('ended',myHandler,false); 
   
  function myHandler(e) { 
      var video = document.getElementsByTagName('video')[0]; 
      var mediaName="13502979:Sailing"; 
      var mediaLength = video.duration; 
      var mediaPlayerName = "HTML5 Player"; 
      /*Define video offset*/ 
      if (video.currentTime > 0) { 
          mediaOffset = Math.floor(video.currentTime); 
      } else { 
          mediaOffset = 0; 
      }; 
      /*Call on video start*/ 
      if (e.type == "play") { 
          if (mediaOffset == 0) { 
              console.log(mediaPlayerName + 
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime)); 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15'; 
              s.linkTrackEvents='event2'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar15=mediaPlayerName; 
              s.events='event2'; 
              s.tl(this,'o','Video Start'); 
          } 
      }; 
   
      /*Call on video pause*/ 
      if (e.type == "pause") { 
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime)); 
          if (video.currentTime != video.duration) { 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15'; 
              s.linkTrackEvents='event7'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar15=mediaPlayerName; 
              s.events='event7'; 
              s.tl(this,'o','Video Pause'); 
          } 
      }; 
   
      /*Call on video complete*/ 
      if (e.type == "ended") { 
          console.log(mediaPlayerName + 
            ' -> ended -> playhead: ' + 
            Math.floor(video.currentTime)); 
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15'; 
          s.linkTrackEvents = 'event3'; 
          s.prop10= m ediaName; 
          s.eVar10=mediaName; 
          s.eVar12="video"; 
          s.eVar13=document.title; 
          s.eVar15=mediaPlayerName; 
          s.events='event3'; 
          s.tl(this,'o','Video Complete'); 
      }; 
  }; 
</script>
```

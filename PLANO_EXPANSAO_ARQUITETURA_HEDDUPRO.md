# DIAGNÓSTICO E MAPEAMENTO DA ARQUITETURA: RADIO HEDDUPRO INDOOR

Data: 15/09/2026
Autor: Eduardo Rodiney I. da Silva (Matricula: 202422892)

=============================================================================
STATUS ATUAL DO PROJETO VS. VISÃO COMPLETA EXPANDIDA
=============================================================================

1. MOTOR DE ÁUDIO E AFINAÇÃO 432Hz:
- Status Atual: Já existe audioEngine.js com tuning432On (linha 455). Atualmente operando com fator de reprodução analógica (432/440 ~ 0.9818) para rebaixamento limpo de afinação sem artefatos de fase WASM.
- O que falta para a visão total: Chave de acionamento dinâmico na interface do operador/cockpit com indicador visual de afinação (A=432Hz vs A=440Hz), além do módulo pitchCheck.js que já faz análise de autocorrelação espectral.

2. CURADORIA POR BPM E PERFIS DE NEGÓCIO:
- Status Atual: Totalmente implementado em segmentProfiles.js e radioDirector.js. Já possui bloqueio de músicas lentas/piano fora da madrugada (0h-6h) e regras rígidas por segmento (mercado, academia, farmácia).
- O que falta para a visão total: Exposição clara do slider e target de BPM por período no cockpit (ex: Modo Acolhimento 60-75 BPM, Modo Almoço/Pico 110-128 BPM).

3. MUSICOTERAPIA E PROTEÇÃO SENSORIAL (TEA / TDAH):
- Status Atual: segmentProfiles.js já possui listas de exclusão de termos agressivos e segmentações relaxantes (spa, consultório, clínica).
- O que falta para a visão total: Preset 'Modo Sensorial Seguro / TEA-TDAH' que ativa corte de altas frequências agressivas no Master EQ (10 bandas), compressor limitador com ratio suave e restrição a transientes rítmicos abruptos.

4. SISTEMA DE ADS CRUZADOS E GERAÇÃO VIA WHATSAPP:
- Status Atual: No backend existem serviços de creativeAnnouncer.js, aiRoutes.js e modelo Prisma Announcement/Insertion.
- O que falta para a visão total:
  a) Webhook/Endpoint para ingestão de mensagem WhatsApp (Twilio/Baileys/Z-API);
  b) Pipeline de geração automática: IA resume a oferta -> TTS gera a locução comercial com voz Edu/Manú -> Canvas/Sharp renderiza o encarte visual (banner 1920x1080) para exibição na tela do Ambient.jsx.

5. CLUSTER MULTI-DISPOSITIVOS (GRANDE CAIXA DE SOM EM REDE):
- Status Atual: Existe a infraestrutura P2P com p2pMediaMesh.js e WebSockets no Fastify para sincronismo de estado do player.
- O que falta para a visão total: Mecanismo de sincronização de clock via NTP/WebSocket (AudioContext.currentTime offset) para que nós remotos toquem o mesmo chunk de áudio em sincronia de fase sub-milissegundo.

6. HARDWARE FÍSICO, MIDI E ILUMINAÇÃO (DMX/SHOWS):
- Status Atual: Web Audio API implementada e consoles virtuais de mixagem no Cockpit.
- O que falta para a visão total: Web MIDI API listener (navigator.requestMIDIAccess) para mapear faders, botões e knobs físicos diretamente aos canais do audioEngine (Música, Locução, Bergs, Master) e disparar comandos de iluminação DMX via bridge Art-Net/WebSockets.

7. VITRINE CULTURAL PARA MÚSICOS E COMPOSITORES:
- Status Atual: Tabela Track e PedidoMusica no Prisma, integração do Respondeu Ganhou e pedidos ao vivo.
- O que falta para a visão total: Flag 'isAutoral' / 'indieArtist' no catálogo com bloco de rotação obrigatório garantido (ex: 1 faixa independente a cada 45 min) e card na vitrine do Ambient exibindo capa, nome do compositor e QR Code para apoio/redes sociais do artista.

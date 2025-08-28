# Gateway WoofTags — Guia de Configuração

Este guia explica como ligar, acessar e configurar o gateway da WoofTags. Ao final, você terá o Wi-Fi e as credenciais de API salvas, o relógio sincronizado por NTP e poderá acompanhar **logs em tempo real** via navegador.

## O que vem de fábrica

* **AP sempre ativo (AP+STA):** o gateway cria um Wi-Fi próprio para configuração.

  * **SSID:** `Gateway-WoofTags`
  * **Senha:** `12345678`
  * **Canal:** 6
  * **IP do AP:** `192.168.4.1`
* **Portal Web de Configuração:** `http://192.168.4.1/`
* **Autenticação do portal (Basic Auth):**

  * **Usuário:** `admin`
  * **Senha:** `admin`
* **NTP:** sincroniza horário pela internet.
* **Logs:** página `/logs` com atualização em tempo real.

> ⚠️ **Importante:** troque a senha do portal logo após o primeiro acesso (seção “Credenciais de Acesso” no portal).


## Pré-requisitos

* Uma fonte de alimentação/USB para o Gateway.
* Um computador ou celular com Wi-Fi para entrar no AP do gateway.
* Os dados da sua API:

  * `CLIENT_ID`
  * `CLIENT_SECRET`
  * `COMPANY_SLUG`


## Passo a passo

1. **Ligue o gateway.**
   Aguarde \~10s; o AP `Gateway-WoofTags` ficará disponível.

2. **Conecte-se ao AP do gateway.**

   * SSID: `Gateway-WoofTags`
   * Senha: `12345678`

3. **Abra o portal de configuração.**

   * Acesse `http://192.168.4.1/`
   * Faça login (Basic Auth): `admin` / `admin`.

4. **(Opcional, mas recomendado) Troque o usuário/senha do portal.**

   * Em **Access Credentials**, preencha **User** e **Password**.
   * Clique **Save Access**.
   * O dispositivo reinicia e volta para o AP. Reacessar o portal com as novas credenciais.

5. **Configure Wi-Fi & API.**

   * Em **Wi-Fi & API**, informe:

     * **Wi-Fi SSID** e **Wi-Fi Password** da sua rede.
     * **CLIENT\_ID**, **CLIENT\_SECRET** e **COMPANY\_SLUG**.
   * Clique **Save Config**.
   * O dispositivo reinicia para aplicar as configurações.

6. **Confirme a conexão STA.**

   * Reabra `http://192.168.4.1/` (o AP continua ativo).
   * A página mostra:

     * **AP IP** (ex.: `192.168.4.1`)
     * **STA IP** (IP obtido na sua rede Wi-Fi; se “-”, ainda não conectou).


## Verificando em tempo real (Logs)

* Entre em **/logs**:

  * No portal (home), clique em **“Ver LOGs em tempo real”**, ou vá direto para `http://192.168.4.1/logs`.
* Exemplos de logs úteis:

  * `HTTP server started`
  * `STA: <ip>` quando o gateway conectou ao seu Wi-Fi
  * `AUTH -> 200` quando o JWT é obtido com sucesso
  * `PING time / PING config / PING price` quando chegam solicitações
  * `Config sent` com o ciclo de atualização/agenda enviado aos ePapers

## Reset de fábrica

Você pode limpar a configuração (Preferences) e reiniciar:

* **No boot:** mantenha o botão **BOOT** pressionado por **\~5s** enquanto liga o dispositivo.
* **Em runtime:** mantenha o **BOOT** pressionado por **\~30s**.
  Os logs mostrarão a contagem e, ao final, o gateway será reiniciado com configurações de fábrica.

## Dicas & Solução de Problemas

* **Não conectou na sua rede?**

  * Verifique SSID/senha.
  * O AP (`Gateway-WoofTags`) continua disponível — reconfigure pelo portal.
  * Seu roteador precisa permitir **canal 6**.

* **`AUTH -> 401` nos logs?**

  * Revise `CLIENT_ID` e `CLIENT_SECRET`.
  * Confira se o `COMPANY_SLUG` está correto.
  * Note que ao alterar credenciais, o JWT será limpo e refeito no próximo uso.

* **Horário incorreto?**

  * A sincronização NTP requer que o gateway esteja **on-line** (STA conectado).
  * O fuso (offset) padrão é **−03:00** (−180 min) — usado nas respostas de tempo para os ePapers.

* **Sem logs no navegador?**

  * Garanta que fez login no portal.
  * Tente recarregar `/logs`. A página usa SSE (EventSource) — a maioria dos navegadores modernos suporta.
  * Se enxergar `[conexao perdida]`, verifique o Wi-Fi do cliente e do gateway.

---

Pronto! Seu gateway está configurado. Se quiser, posso gerar um checklist impresso ou um QR com o link do portal para facilitar a instalação em campo.

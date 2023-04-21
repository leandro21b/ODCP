# ODCP - Open Digital Contract Protocol

`Portuguese-Brazil`

## Descrição:

A ideia é um mecanismo simples de contratos baseado em json onde um contrato é criado e assinado digitalmente pelas partes envolvidas com uma chave privada que só elas tem, isso prova que as partes realmente aceitaram com o contrato, se alguém tentar alterar qualquer dado no contrato as assinaturas irão dar como inválidas pois elas foram feitas baseada nos parametros originais do contrato, isso torna impossivel de alguém fraudar o contrato e as assinaturas, além disso a verificação das assinaturas pode ser feita de forma instantânea por qualquer dispositivo.

## Aplicações:

Esse protocolo simples pode ser aplicado em qualquer tipo de contrato em qualquer lugar, por exemplo: um contrato de venda de um imovel ou veículo, um casamento, um contrato entre moradores de uma vizinhança, ou até um contrato aeroespacial multibilhonário, não importa tudo isso são contratos, "Pacta Sunt Servanda" Contratos fazem lei entre as partes e esse protocolo pode ajudar muito na criação de bons contratos seguros e facilmente verificaveis, esse protocolo também pode contribuir muito para a justiça descentralizada que é justamente baseada em contratos voluntários, esse será a lei.

## Armazenamento:

O contrato pode ser armazenado pelas partes envolvidas, em servidores de terceiros, na rede Nostr colocando o contrato em json dentro de um evento nostr como se fosse uma caixa dentro de outra caixa, ou até dependendo da importância do contrato na prórpia Timechain do Bitcoin através do protocolo ordinals ou vários OP_RETURN, os contratos podem ser publicos para qualquer um ver e verificar ou privado onde o contrato é criptografado e só as partes autorizadas podem descriptografá-lo e ver o seu conteúdo, todo o contrato pode ser criptografado ou só a parte do conteúdo do contrato por exemplo.

## Alterações posteriores no contrato:

Para que uma alteração seja feita todas as partes envolvidas no contrato dever aceitar essa alteração, existem 2 formas de se fazer isso com a primeira sendo simplesmente alterar os dados e pedir para as partes reassinarem o contrato, e a segunda é fazer os mesmos passos mas colocando no campo `Addition` uma referência ao ID do contrato anterior com `R` que significa substituição, ou `C` que significa complemento

## Adições:

O contrato pode ter adições como vídeos, imagens, audios, etc, nesse caso deverá ser referênciado no campo `Addition` o Hash do arquivo. o contrato em si não inclui esses arquivos por serem muito pesados, eles podem estar juntos na pasta do contrato, em uma url, na rede Bittorrent, etc. Mas como a assinatura depende do hash do contrato que por sua vez depende dos dados o que inclui o hash do arquivo, tecnicamente o conteudo desse arquivo também será assinado ainda que indiretamente.

## Exemplo simples:

```json
{
    "ID": "7f1ce9a2f8ced5e804d430ccfd2013edc007c79f2bc26605ebc091eda7b15699",
    "Title": "Freedom Street construction contract",
    "Kind": "Service Contract",
    "Parties": [
        [
            "Cidade Privada Cypherpunk",
            "npub1usxgl3mwpnykar3k3gwkekczn76jd2dxw0f5xdcxh4dwlm6yy6kqudq0eh",
            "Y"
        ],
        [
            "Satoshi Roads",
            "npub1z7p2u0ylx9jwprqhjq2m4p6ckp9p3zsxzne342qelkatc8ycaapq7fr6ma",
            "Y"
        ]
    ],
    "Contract": "A 'Cidade Privada Cypherpunk' esta contratando a empresa 'Satoshi Roads' para construir a rua 'Freedom Street', o termino das obras devera ser no dia 27 de abril e a inauguracao no dia seguinte, as clausulas sao [...], o orcamento e de 20 BTC",
    "Time": "1682001135",
    "Duration": "Until: 28/04/2023",
    "Addition": [],
    "Sigs": [
        "afc923397292b6a52489dd9c2e1e8e3cc0ee5dbd492c28cd05fb4398c20f40dab5a73e7466b2853f6ab2e8423ed19a01cc24994147a4c89d81fdb966c40b6fed",
        "07efcfd6539bd248f3309147ba82745201545cb609bd32851397e15b9e495ef926ec425334d59b0a9ade37fc5a650d9fa556662cdc0e75f522c7fbf62f303d86"
    ]
}
```

Nesse exemplo fica provado que a empresa Satoshi Roads se compromete a construir uma estrada para a Cidade Privada Cypherpunk, se houver algum problema fica fácil de provar e as assinaturas digitais provam que todos os envolvidos realmente aceitaram as clausulas do contrato.

Claro que esse exemplo é bem simples, na vida real o contrato vai ser bem mais complexo.

## Exemplo de casamento:

```json
{
    "ID": "9e9ba62a2f06bc03a19761edecd099852cf1c51621d28c7178623edda9225c04",
    "Title": "Casamento de Love & Baby",
    "Kind": "Marriage",
    "Parties": [
        [
            "Love",
            "npub14fu7cyyml5cccyv9vwnpdt4em2sfssf574hs7vxhsl2y9z2xkppq4x2dz6",
            "Y"
        ],
        [
            "Baby",
            "npub1vp3axsn0ke6ale4f06ml2vmndlztswdpzesa6fxs3v2w08cyp0xsfkdhqg",
            "Y"
        ]
    ],
    "Contract": "Love e Baby se comprometem a estarem juntos, buscar novos caminhos juntos e serem honestos um com o outro [...]",
    "Time": "1681926031",
    "Duration": "Forever",
    "Addition": [],
    "Sigs": [
        "09650df17abba1c55ce11c44c583bec38920362a966cd1f0408b74cf8b1176e06eecdfd39b51f30e297f6d32bb796e89e10b517e35090ac7690770dbaab91bc2",
        "e070baac091473be534093699c7aff842a0e7bbc7f23cc05d5908b11ecb6e126f1fa988fc5a1b302c968c0b6816c38d9530f2beddab437461597ed2989cfcefb"
    ]
}
```

O importante é o contrato assinado pelo casal, essa será a lei válida entre eles, qualquer tipo de contrato pode ser criado com o ODCP e isso cria várias possibilidades que podem inclusive substituir sistemas burocráticos como cartórios por exemplo se as pessoas aderirem a ideia.

## Mais detalhes do protocolo:

#### Partes envolvidas:
Os participantes de um contrato são declarados em `Parties`, lá é declarado o nome ou pseudonimo da pessoa ou empresa envolvida, depois uma chave publica, pode ser `nopubkey` se a pessoa não tiver chave pública (nesse caso ela não poderá assinar o contrato), e depois se a assinatura é exigida ou não dessa parte, não há limite de participantes no contrato.

`Y` = assinatura obrigatória

`N` = assinatura não obrigatória

`Y<timestamp>` = assinatura obrigatória depois de uma data especifica

#### Chaves publicas e privadas:
O algoritomo de chaves é o `secp256k1` e as chaves tem o mesmo formato `bech32` do `Nostr`, com a publica começando com `NPUB` e a privada com `NSEC`, a chave publica é usada para identificação e validação da assinatura, a chave privada é usada para assinar e provar que é realmente o dono da chave publica que assinou o contrato, a chave privada pode ser derivada de uma seed de 12 palavras que o dono pode até memorizar.

#### Assinaturas e hash:
O algoritomo usado nas assinaturas é o `Schnorr` e as assinaturas são feitas a partir no hash do contrato que é um `sha256` que é tirado de todos os dados do contrato como as partes envolvidas, o conteudo em si, o timestamp, e outros dados, o ID é o hash de todos os dados do contrato.

#### Campo `Duration`:
Determina até quando o contrato é valido, se for `forever` significa que é para sempre, pode ser `undefined` ou seja indefinido, pode ser colocado um timestamp da data que o contrato expira, uma data em claro ex: 03/01/2009, 18:15:05, etc.

#### Campo `Adittion`:
Esse campo pode ser usado para referênciar outros contratos ou adicionar informações extras como por exemplo: hash de arquivos relacionados ao contrato como vídeos, imagens, audios, etc. também pode ser usado para referênciar substituição de um contrato anterior ou complemento desse, etc.

`["R", <id contrato anterior>]` `R` = que substitui o contrato anterior

`["C", <id contrato anterior>]` `C` = complemento do contrato anterior

`["F", <id do arquivo>]` `F` = file ou arquivo

## Softwares:

Quando houver softwares disponíveis eles serão exibidos aqui, no momento estamos desenvolvendo a primeira aplicação para esse novo protocolo.

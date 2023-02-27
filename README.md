ansible role to insert debian 11 in samba as domain member

## troubleshooting

Um grupo "estranho" foi criado do DC chamado: $e6d5cd9d-9ac5fa1db74874b3 e propagado para o membros do domínio. No membro, rodando o comando *wbinfo -g* via-se o grupo problemático. Ainda no membro podemos ver os grupos de um usuário *12688070* com o comando:

    # id 12688070@dmbdomain.fflch.usp.br

O usuário 12688070 não consegui logar, enquanto que o usuário 5385361 conseguia. Comparando-se os grupos:

    # id 5385361@smbdomain.fflch.usp.br
    
Percebemos que o usuário *12688070* pertencia ao grupo $e6d5cd9d-9ac5fa1db74874b3 e não conseguia logar e o 5385361 não pertencia e o login estava normal. Para corrigir, o grupo foi deletado no DC:

    samba-tool group delete '$E6D5CD9D-9AC5FA1DB74874B3'


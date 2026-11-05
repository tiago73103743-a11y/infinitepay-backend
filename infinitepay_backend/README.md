# Loja + InfinitePay

## Como colocar no ar

1. No aplicativo InfinitePay: **Vendas → Checkout → Configurações → Habilitar Checkout Integrado**. Encontre sua **InfiniteTag** sem `$`.
2. Implante a pasta `infinitepay_backend` em hospedagem Node.js (o GitHub Pages **não** executa Node).
3. Configure as variáveis de ambiente no provedor de hospedagem:
   - `INFINITEPAY_HANDLE`: sua InfiniteTag sem `$`.
   - `SITE_ORIGIN`: URL exata do seu GitHub Pages, somente domínio/origem, ex.: `https://usuario.github.io`.
   - `INFINITEPAY_API_KEY`: chave secreta **opcional**, criada na InfinitePay. Necessária para descontos PIX automáticos e link de uso único. Nunca coloque no HTML/GitHub.
   - `DESCONTO_PIX`: ex.: `5` (somente com API Key; desconto aplicado pela InfinitePay, não pelo HTML).
4. No arquivo `catalogo.json`, cadastre **cada produto com ID e preço em centavos** igual ao site. Ex.: produto 1 de R$18 = `1800`. Toda mudança de preço feita no site precisa ser refletida no catálogo seguro do backend; caso contrário, a cobrança será feita pelo preço do servidor. O sistema rejeita produtos sem cadastro.
5. No HTML, entre como administrador → Configurações → Endereço do servidor InfinitePay. Salve a URL https do backend. O PIX manual antigo permanece opcional.
6. A compra abre o checkout seguro da InfinitePay, onde o cliente escolhe Pix ou cartão e o QR Code é gerado pela InfinitePay.

**Atenção:** a integração está preparada mas não há cobrança ativa até você configurar e hospedar o backend e o catálogo. A InfinitePay não fornece ambiente sandbox; faça um teste controlado de valor baixo quando estiver pronto. **Este exemplo não confirma pedidos automaticamente**. Para colocar em produção, implemente persistência de pedidos em banco de dados e validação de eventos de pagamento com `/payment_check` no backend antes de liberar mercadorias. Também implemente gestão de estoque e administração segura no servidor. O login de administrador do HTML atual não protege o backend. Não use a senha fixa do HTML para produção.

Documentação: https://www.infinitepay.io/checkout-documentacao

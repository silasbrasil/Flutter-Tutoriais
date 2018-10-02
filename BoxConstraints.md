# Lidando com Box Constraints em Flutter

Esse tutoria é uma introdução à Box Constraints (Restrições de Caixa). Mas o que realmente isso significa? Box Constraints é uns dos principais assuntos no que tange o layouts em Flutter. No desenvolvimentos de UI temos que lidar com restrições de tamanho e flexibilidade dos componentes (Widgets) na tela do dispositivo o tempo todo. Flutter tenta nos ajudar a fazer isso. Mesmo assim, não é tão trivial.

No Flutter, os Widgets são renderizados pelo objeto `RenderBox`. As Render Box recebem restrições que são passadas pelo Widget pai, e se redimencionam com base nessas restrições. Restrições consistem em larguras e alturas máximas e mínimas; já o tamanho consistem em uma largura e altura específica. Ou seja, por mais que um Widget tenha um tamanho específico, suas retrições podem se diferentes do seu tamanho. Espero que mais a frente isso fique mais claro.

### Widgets com RenderBox básicos
Em termos de como as RenderBox dos Widgets tratam suas restrições (Constraints), abaixo seguem os três de mais baixa complexidade.

  - Os que tentam ser o maior possível. Por exemplo, `Center` e `ListView`.
  - Os que tentam ser do tamanho do seus filhos. Por exemplo, `Transform` e `Opacity`.
  - Os que tentam ser de um tamanho particular. Por exemplo, `Image` e `Text`.

###### Variante 1
A RenderBox do Widget `Container` varia seu comportamento baseado nos parâmetros que são passados no seu construtor. Por padrão, ela tenta ser o maior possível, mas se é passado uma largura no parâmetro __width__ ele tenta respeitar essa largura.

###### Variante 2
Outras, por exemplo `Row` e `Column` são do tipos (Flex Box) e variam com base do filhos que lhes são passados. Esses casos serão discutidos abaixo seção __Flex Box__.

###### Variante 3
Já sobre as constraints, há ainda as do tipo __"tight"__ (ajustada). Elas não deixam que as RenderBox decidam o seu tamanho. Por exemplo, se as larguras mínima e máxima são as mesmas, diz-se que tem uma largura do tipo __"tight"__. O principal exemplo disso é o widget App, que é contido pela classe `RenderView`: a caixa usada pelo filho retornado pela função `build` do aplicativo recebe uma restrição que o força a preencher exatamente toda a área de conteúdo do aplicativo (geralmente, a tela inteira). Muitas das caixas em Flutter, especialmente aquelas que recebem apenas um filho único, passam sua restrição para seus filhos. Isso significa que, se você aninhar um monte de caixas desse tipo, uma dentro uma da outra, desde a raiz da árvore de renderização do seu aplicativo, todas elas se encaixarão exatamente uma na outra, forçadas por essas restrições do tipo tight.
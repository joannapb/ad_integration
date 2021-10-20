# Documentação para a Importação de Anúncios da OLX Brasil

A OLX hoje suporta dois tipos de importação de anúncios, para anunciantes que querem gerenciar seus anúncios a partir de um software terceiro (ou seja, sem passar pelas interfaces nativas da OLX para gestão de inventário): via API ou via arquivo (JSON ou XML).


## Status das Integrações da OLX

| Modelo de Integração | Versão em produção | Categorias atendidas | Próximos passos |
|----------------------|----------------------------|----------------------|---------------------------------------------------------------------------------------|
| [API](api/README.md) | Estável | Autos e Imóveis | Escrever documentação de categorias não-documentadas. Preparar comunicação e rollout da Fase 2 da nova API de Integração de Anúncios. |
| [XML](xml/real_estate/README.md) | Estável | Imóveis | Nenhuma evolução prevista. Documentação atualizada.


## Categorias Suportadas por cada Modelo de Integração

Nem todas as categorias de anúncios na OLX são suportadas pelas integrações existentes:

| Categoria | Subcategoria | XML | API |
|-------------------------|-----------------------------------------|-----|-----|
| Imóveis | Apartamentos | [Sim](xml/real_estate/README.md) | [Sim](api/real_estate/README.md) |
| Imóveis | Casas | [Sim](xml/real_estate/README.md) | [Sim](api/real_estate/README.md) |
| Imóveis | Aluguel de quartos | Não | Sim  |
| Imóveis | Temporada | Não | Sim  |
| Imóveis | Terrenos sítios e fazendas | [Sim](xml/real_estate/README.md) | [Sim](api/real_estate/README.md) |
| Imóveis | Comércio e indústria | [Sim](xml/real_estate/README.md) | [Sim](api/real_estate/README.md) |
| Autos e peças | Carros vans e utilitários | Não | [Sim](api/autos/README.md) |
| Autos e peças | Motos | Não | [Sim](api/autos/README.md) |
| Autos e peças | Ônibus | Não | Sim |
| Autos e peças | Caminhões | Não | Sim |
| Autos e peças | Barcos e aeronaves | Não | Sim |
| Peças e acessórios | Carros vans e utilitários | Não | [Sim](api/autoparts/README.md) |
| Peças e acessórios | Motos | Não | [Sim](api/autoparts/README.md) |
| Peças e acessórios | Ônibus | Não | [Sim](api/autoparts/README.md) |
| Peças e acessórios | Caminhões | Não | [Sim](api/autoparts/README.md) |
| Peças e acessórios | Barcos e aeronaves| Não | [Sim](api/autoparts/README.md) |


## Perguntas e Dúvidas Frequentes

Algumas das principais dúvidas relativas à integração de anúncios com a OLX podem ser vistas aqui:

- [Mudança de categoria de anúncios](faq/category.md)
- [Especificações para imagens dos anúncios](faq/images.md)
- [Inferência de Inserção, Edição e Deleção de Anúncios em Integrações via XML ou JSON](faq/xml_json_insertion.md)


## Dúvidas, Sugestões e Comentários

Caso você queria um suporte para sua integração, pode enviar email para suporteintegrador@olxbr.com.

**Importante**: Esta documentação está focada na importação de anúncios para o portal OLX Brasil. Para importação de anúncios para os portais Autoshift e Storia Imóveis, contate suporteintegrador@olxbr.com.

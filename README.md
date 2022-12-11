# 基于GlobalPointer的命名实体识别

#### NER任务
    
       命名实体识别（NER）是自然语言处理（Natural Language Processing，NLP）领域的一项基本的任务，
    长久以来一直得到学术界和产业界的广泛研究和关注，其在很多应用中已经成为不可或缺的步骤。
       
       NER任务分解通常包括两部分，分别是实体的边界识别和实体类型的确定（通用的实体类型包括人名、地名、机构名、时间或其他），
    因此如何提升实体的边界识别和实体类型的识别效果是NER任务研究的关键问题。
    
       目前学术研究主要将NER任务主要分为3类，包括
            扁平化NER（Flat NER），指的是从输入文本中抽取连续的实体片段和其所对应的实体类型；
            嵌套NER（Nested/Overlapped NER），指的得是从文本中抽取的两个或多个实体，其文本片段之间存在一部分的文字重叠；
            非连续NER（Discontinuous NER），指的是从文本中所抽取的实体间存在多个片段，且片段之间不相连，存在其他文本间隔。
    
#### NER方法
    1.传统NER方法
       基于序列标注的方法是 Flat NER的基准模型，主要对实体的每一个token分配标签进行标注，标注方式如BIO、BIEOS等。
    目前比较主流的方法是将CRF模型与神经网络模型进行结合，最后通过CRF层进行预测结果的全局优化。
       缺点：传统NER方法将NER作为序列标注问题，只能在单个的序列scan的文本中识别没有重叠的实体，但是不能识别嵌套的实体和非连续实体，
            主要原因是很难为所有的NER任务设计一个通用的标注方案。
    2.基于span的方法
       基于SPAN的方法主要思想是列举所有可能的span，并确定它们是否是有效的实体和类型。
       方法主要使用包括指针网络或者token对的形式聚焦于实体边界的识别，具体实现如分别设置start指针和end指针，表示实体的开始和结束位置信息。
       缺点：实体长度太长，导致模型复杂度较高，无法处理非连续实体。
    3.GlobalPointer方法
       基于多头选择的NER统一模型，可以处理扁平、嵌套。
       模型         F1
       gp      0.7343827980024905, 0.898337720638375, 0.9005195469741897, 0.9050500051460093, 0.9090611447884819, 0.9248531106509561, 0.9202409999856301, 0.9123682104457549, 0.9285823407039423, 0.9284797043562025
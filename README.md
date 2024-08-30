# function_recursive


function calculateRemainingQuantity(quantityTab, qtyEntered, i = 0) {
                            if (i >= quantityTab.length || qtyEntered <=0) {
                                console.log("Quantité restante :", qtyEntered)
                                if(qtyEntered>0){
                                    dataToPatch.DocumentLines.push({
                                        BaseType: 22,
                                        Quantity: qtyEntered
                                    })
                                }
                                return qtyEntered
                            }
                            let qtyRemaining = qtyEntered - quantityTab[i]
                            if (qtyRemaining < 0) {
                                console.log(`Index: ${i}, Quantité validée: ${qtyEntered}, Quantité restante: 0`)
                                qtyRemaining = 0
                                    dataToPatch.DocumentLines.push({
                                        BaseType: 22,
                                        BaseEntry: DocEntry,
                                        BaseLine: LineNum[i],
                                        Quantity: qtyEntered
                                    })
                            } else {
                                console.log(`Index: ${i}, Quantité validée: ${quantityTab[i]}, Quantité restante: ${qtyRemaining}`)
                                    dataToPatch.DocumentLines.push({
                                        BaseType: 22,
                                        BaseEntry: DocEntry,
                                        BaseLine: LineNum[i],
                                        Quantity: quantityTab[i]
                                    })
                            }
                            console.log("index", i)
                            return calculateRemainingQuantity(quantityTab, qtyRemaining, i + 1)
                        }
                        let qtyRemaining = calculateRemainingQuantity(quantityTab, QtyEntered)
                        console.log("Quantité restante finale :", qtyRemaining)
                        console.log("dataToPatch :",dataToPatch)
                        Models.Drafts().patch(dataToPatch, DocEntry)
                        dialog.close()

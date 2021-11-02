# pillar-algorithms-for-optimizations-
#fungsi pillar
def pillar(data,k,alfa,beta):
  C = []; SX = []; X = np.array(data)
  n = len(data)
  DM = np.array([0.]*n)
  
  #-----------------------
  m = np.mean(X) #hitung nilai tengah (mean)
  #-----------------------

  D = np.sqrt((X-m)**2) #hitung jarak objek data dengan median # untuk mencari jarak menggunakan rumus eucledien distance (agar hasil pasti positif karena di kuadrat kemudian diakarkan)
  nmin = alfa*n/k #nilai nmin
  dmax = np.argmax(D)
  nbdis = beta*dmax
  
  for i in range(k):
    DM = DM + D
    oi = 0 #buat ngecek iterasi
    while True :
      #print("lendm =",len(DM)) 
      #print("nmin =",nmin)
      #print("nbdis =",nbdis)
      xx = np.argmax(DM)
      ##print("xx =",xx)
      SX = list(set().union(SX, [xx])) #union 
      #print("SX = ",SX)
      D = np.sqrt((X-X[xx])**2)
      
      no = len([D[j] for j in range(len(D)) if D[j] <= nbdis])
      #print("no =", no)
      
      #DM = [0 for j in range(len(DM))if j == xx]
      for j in range(len(DM)):
        if j==xx:
          DM[j] = 0
      if no >= nmin:
        break
      oi+=1
      #print("looping ke",oi) 
    #D = [0 if j == k else D[j] for j in range(len(D)) for k in SX]
    for j in range(len(D)):
      for k in SX:
        if j == k:
          D[j] = 0
    C.append(xx)
  return C
